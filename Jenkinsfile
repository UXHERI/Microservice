pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker build -t adijaiswal/emailservice:latest ."
                    }
                }
            }
        }
        stage('Tag for My Repo') {
            steps {
                script {
                    sh "docker tag adijaiswal/emailservice:latest uxheri/emailservice:latest"
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push uxheri/emailservice:latest "
                    }
                }
            }
        }
    }
}
