pipeline {
    agent any // Runs the pipeline on any available agent

    stages {
        stage('Deploy To Kubernetes') { 
            steps {
                // Uses Kubernetes credentials to apply deployment configuration
                withKubeCredentials(kubectlCredentials: [[
                    clusterName: 'EKS-2',
                    credentialsId: 'k8-token',
                    namespace: 'webapps',
                    serverUrl: 'https://93E7C4D024D8ED9307306ACB21004F5A.gr7.eu-west-2.eks.amazonaws.com'
                ]]) {
                    sh "kubectl apply -f deployment-service.yml"
                }
            }
        }
        
        stage('Verify Deployment') { 
            steps {
                // Uses Kubernetes credentials to check the status of deployed services
                withKubeCredentials(kubectlCredentials: [[
                    clusterName: 'EKS-1',
                    credentialsId: 'k8-token',
                    namespace: 'webapps',
                    serverUrl: 'https://93E7C4D024D8ED9307306ACB21004F5A.gr7.eu-west-2.eks.amazonaws.com'
                ]]) {
                    sh "kubectl get svc -n webapps"
                }
            }
        }
    }
}
