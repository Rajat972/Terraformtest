pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'java11'
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

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
