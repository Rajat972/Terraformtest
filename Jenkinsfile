pipeline {
    agent any

    stages {

        stage('Deploy to TEST') {
            steps {
                sshagent(['ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.19.114 \
                    "echo 'Hello from TEST server 🚀'"
                    '''
                }
            }
        }

        stage('Approval for PROD') {
            steps {
                input message: 'Deploy to PROD?'
            }
        }

        stage('Deploy to PROD') {
            steps {
                sshagent(['ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.21.91 \
                    "echo 'Hello from PROD server 🔥'"
                    '''
                }
            }
        }
    }
}
