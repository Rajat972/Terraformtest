pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {


        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to DEV') {
            steps {
                sshagent(['ssh-key']) {
                    sh '''
                    ssh ubuntu@172.31.19.114 "
                        sudo rm -rf /var/lib/tomcat10/webapps/myapp*
                    "

                    scp target/*.war ubuntu@172.31.19.114:/tmp/

                    ssh ubuntu@172.31.19.114 "
                        sudo mv /tmp/*.war /var/lib/tomcat10/webapps/ &&
                        sudo chown tomcat:tomcat /var/lib/tomcat10/webapps/*.war &&
                        sudo systemctl restart tomcat10
                    "
                    '''
                }
            }
        }

        stage('Approval for PROD') {
            steps {
                input message: 'Deploy WAR to PROD?'
            }
        }

        stage('Deploy to PROD') {
            steps {
                sshagent(['ssh-key']) {
                    sh '''
                    ssh ubuntu@172.31.21.91  "
                        sudo rm -rf /var/lib/tomcat10/webapps/myapp*
                    "

                    scp target/*.war ubuntu@172.31.21.91:/tmp/

                    ssh ubuntu@172.31.21.91  "
                        sudo mv /tmp/*.war /var/lib/tomcat10/webapps/ &&
                        sudo chown tomcat:tomcat /var/lib/tomcat10/webapps/*.war &&
                        sudo systemctl restart tomcat10
                    "
                    '''
                }
            }
        }
    }
}
