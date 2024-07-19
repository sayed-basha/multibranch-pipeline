
pipeline {
    agent any

    stages {
        stage('build war file') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    dir('target') {

                    withDockerRegistry(credentialsId: 'github-creds') {
                        sh "docker build -t basha999/lightblue:v$BUILD_NUMBER ."
                    }
                        }
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'github-creds') {
                        sh "docker push basha999/lightblue:v$BUILD_NUMBER "
                    }
                }
            }
        }
    }
}
