pipeline {
    agent any // Runs the pipeline on any available agent

    stages {
        stage('Deploy To Kubernetes') { // Defines the first stage for deploying to Kubernetes
            steps {
                // Uses Kubernetes credentials to apply deployment configuration
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://934C999B89F9E6D0AFC1C30ED9FC8AD6.gr7.ap-south-1.eks.amazonaws.com']]) {
                }
                    
                    sh "kubectl apply -f deployment-service.yml"
                    
                }
            }
        }
        
        stage('verify Deployment') { // Defines the second stage for verifying the deployment
            steps {
                // Uses Kubernetes credentials to check the status of deployed services
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://934C999B89F9E6D0AFC1C30ED9FC8AD6.gr7.ap-south-1.eks.amazonaws.com']]) {
                    // Retrieves information about services deployed in the 'webapps' namespace
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
