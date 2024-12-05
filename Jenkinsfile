pipeline {
    agent any

    stages {
        stage('deploy-to-k8s') {
            steps {
                withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://964EE728558A3230C13DBAEEF7DD5F18.gr7.ap-south-1.eks.amazonaws.com']]) {
                    sh "kubectl apply -f deployment-service.yml" 
                    sleep 60
                }
            }
        }
        
        stage('verify deployment') {
            steps {
               withKubeCredentials(kubectlCredentials: [[caCertificate: '', clusterName: 'EKS-1', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', serverUrl: 'https://964EE728558A3230C13DBAEEF7DD5F18.gr7.ap-south-1.eks.amazonaws.com']]) {
                  sh "kubectl get all -n webapps"
               }       
            }
        }
        
    }
}
