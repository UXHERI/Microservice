pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t adijaiswal/adservice:latest ."
                    }
                }
            }
        }
        stage('Tag for My Repo') {
            steps {
                script {
                    sh "docker tag adijaiswal/adservice:latest uxheri/adservice:latest"
                }
            }
        }        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push uxheri/adservice:latest "
                    }
                }
            }
        }
    }
}
