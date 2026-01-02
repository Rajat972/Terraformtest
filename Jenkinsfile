pipeline {
    agent any

    /*
    tools {
        maven 'maven'
    }

    environment {
        MAVEN_OPTS = "-Xmx512m"
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Test') {
            steps {
                sh '''
                scp target/*.war ubuntu@172.31.19.114:/var/lib/tomcat10/webapps/
                '''
            }
        }

        stage('Approval for Prod') {
            steps {
                input message: 'Deploy to Production?'
            }
        }

        stage('Deploy to Prod') {
            steps {
                sh '''
                scp target/*.war ubuntu@172.31.21.91:/var/lib/tomcat10/webapps/
                '''
            }
        }
    }
