pipeline {
    agent any
    environment {
        // Tell Jenkins where the ubuntu user's Minikube config is located
        MINIKUBE_HOME = '/home/ubuntu'
        KUBECONFIG = '/home/ubuntu/.kube/config'
    }
    stages {
        stage('Clone Code') {
            steps {
                checkout scm
            }
        }
        stage('Build & Deploy') {
            steps {
                // 1. Build the Docker image locally on the EC2 instance
                sh 'docker build -t myapp:latest .'
                
                // 2. Load the image directly into Minikube's internal registry
                sh 'minikube image load myapp:latest'
                
                // 3. Deploy the application to Kubernetes
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}