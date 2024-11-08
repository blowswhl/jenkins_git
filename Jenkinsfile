pipeline {
    agent any
    environment {
 	 ANSIBLE_SSH_ARGS = "-o StrictHostKeyChecking=no"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master',
                    credentialsId: 'github_jenkins_token',
                    url: 'https://github.com/blowswhl/jenkins_git'
            }
        }

        stage('Copy Inventory to Master Node') {
            steps {
                script {
                    sh 'ansible -i /var/lib/jenkins/workspace/jenkins-github-webhook/ansible-inventory.ini loadbalancer -m copy -a "src=/var/lib/jenkins/workspace/jenkins-github-webhook/ansible-playbook.yml dest=/home/user1/ansible/ansible-playbook.yml"'
                }
            }
        }
	stage ('push Docerfile') {
	  //dockerfile build and push 
	   steps {
	       script {
                   docker.build('blowswhl/cicdtest:latest')
		   docker.image('blowswhl/cicdtest:latest').push() 

	       }

	   }

	}

	stage ('start ansible-play book') {
            steps {
	    	script {
                   sh 'ansible-playbook -i /var/lib/jenkins/workspace/jenkins-github-webhook/ansible-inventory.ini loadbalancer /home/user1/ansible/ansible-playbook.yml'

		}

	    }

	}



    }
}
