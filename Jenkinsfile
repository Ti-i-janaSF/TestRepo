pipeline {
    agent any

    environment {
	KUBECONFIG = '/var/jenkins_home/.minikube-ca/config'  // Path to kubeconfig if you have copied it
        CA_CERT_PATH = '/var/jenkins_home/.minikube-ca.crt'        
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }


        stage('Deploy to Minikube') {
            steps {
                script {
		    sh 'kubectl config set-cluster minikube --certificate-authority=${CA_CERT_PATH}'
                    // Apply the Kubernetes YAML files
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }

    }

    post {
        always {
            // Cleanup steps or notifications can go here
            echo 'Cleaning up...'
            sh 'minikube stop'
        }
    }
}
