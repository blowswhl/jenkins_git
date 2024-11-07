pipeline {
    agent any
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
                    sh 'ansible -i /var/lib/jenkins/workspace/jenkins-github-webhook/ansible-inventory.ini loadbalancer -m copy -a "src=/var/lib/jenkins/workspace/jenkins-github-webhook/ansible-inventory.ini dest=/home/user1/ansible/ansible-inventory.ini"'
                }
            }
        }
    }
}
