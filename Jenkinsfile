pipeline {
    agent any // Runs the pipeline on any available agent

    stages {
        stage('Deploy To Kubernetes') { 
            steps {
                // Uses Kubernetes credentials to apply deployment configuration
                withKubeCredentials(credentialsId: 'k8-token') {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }
        
        stage('Verify Deployment') { 
            steps {
                // Uses Kubernetes credentials to check the status of deployed services
                withKubeCredentials(credentialsId: 'k8-token') {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
