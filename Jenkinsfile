pipeline {
    agent any

    environment {
        KUBECONFIG = '/home/jenkins/.kube/config' // Path to the kubeconfig file on Jenkins server
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Set Up Minikube') {
            steps {
                script {
                    // Start Minikube (make sure Minikube is already running or adjust this as needed)
                    sh 'minikube start'
                }
            }
        }

        stage('Deploy to Minikube') {
            steps {
                script {
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
