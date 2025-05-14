pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
    }

    stages {
        stage('Deploy To Kubernetes') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-creds',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    withKubeCredentials(kubectlCredentials: [[
                        caCertificate: '',
                        clusterName: 'EKS-1',
                        contextName: '',
                        credentialsId: 'k8-token',
                        namespace: 'webapps',
                        serverUrl: 'https://099321E17EE35EA8B6A8A602FEA9D19B.gr7.us-east-1.eks.amazonaws.com'
                    ]]) {
                        sh '''
                            export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                            export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
                            export AWS_REGION=$AWS_REGION

                            echo "Deploying..."
                            kubectl apply -f deployment-service.yml
                        '''
                    }
                }
            }
        }

        stage('verify Deployment') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'aws-creds',
                        usernameVariable: 'AWS_ACCESS_KEY_ID',
                        passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                    )
                ]) {
                    withKubeCredentials(kubectlCredentials: [[
                        caCertificate: '',
                        clusterName: 'EKS-1',
                        contextName: '',
                        credentialsId: 'k8-token',
                        namespace: 'webapps',
                        serverUrl: 'https://099321E17EE35EA8B6A8A602FEA9D19B.gr7.us-east-1.eks.amazonaws.com'
                    ]]) {
                        sh '''
                            export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                            export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
                            export AWS_REGION=$AWS_REGION

                            echo "Verifying service..."
                            kubectl get svc -n webapps
                        '''
                    }
                }
            }
        }
    }
}
