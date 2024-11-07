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
                    sh 'ansible -i /var/lib/jenkins/workspace/jenkins-github-webhook/inventory.ini loadbalancer -m copy -a "src=/home/user1/ansible/inventory.ini dest=/desired/path/ansible-inventory.ini"'
                }
            }
        }
    }
}
