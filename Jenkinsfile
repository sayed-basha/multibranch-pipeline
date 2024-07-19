pipeline {
    agent any
    tools {
        maven 'Maven 3.9.8'
    }

    stages {
        stage('build war file') {
            steps {
                sh '/opt/maven/bin/mvn clean install'
            }
        }
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    dir('target') {

                    withDockerRegistry(credentialsId: 'github-creds') {
                        sh "docker build -t basha999/blue:v$BUILD_NUMBER -f Dockerfile ."
                    }
                        }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'github-creds') {
                        sh "docker push basha999/blue:v$BUILD_NUMBER "
                    }
                }
            }
        }
    }
}
