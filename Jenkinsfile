pipeline {
    agent any

    environment {
        # Use the kubeconfig we set up for Jenkins
        KUBECONFIG = '/var/lib/jenkins/.kube/config'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/DollySingarapu/devops-beginner-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh """
                        docker build -t devops-beginner:latest .
                    """
                }
            }
        }

        stage('Deploy to Minikube') {
            steps {
                script {
                    sh """
                        # Check kubectl access
                        kubectl get nodes
                        
                        # Apply Kubernetes manifests
                        kubectl apply -f deployment.yaml
                        
                        # Optional: show pods
                        kubectl get pods
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment to Minikube succeeded!"
        }
        failure {
            echo "❌ Deployment failed. Check logs!"
        }
    }
}
