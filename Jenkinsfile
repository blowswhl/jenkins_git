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
	         withCredentials([usernamePassword(credentialsId: 'Docker_login', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
		   sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD" 
		   }
		   	def image = docker.build('blowswhl/cicdtest:latest')
		   	image.push()

	       }

	   }

	}

	stage ('start ansible-play book') {
            steps {
	    	script {
                   sh 'ansible-playbook -i /home/user1/ansible/ansible-inventory.ini /home/user1/ansible/ansible-playbook.yml'

		}

	    }

	}



    }
}
