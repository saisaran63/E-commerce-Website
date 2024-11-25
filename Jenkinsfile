pipeline {
    agent any

    stages {
        stage('Deploy To Kubernetes') { 
            steps {
                // Use Kubernetes credentials to apply deployment configuration
                withKubeCredentials(credentialsId: 'k8-token') {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }

        stage('Verify Deployment') { 
            steps {
                // Use Kubernetes credentials to check the status of deployed services
                withKubeCredentials(credentialsId: 'k8-token') {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
