pipeline {
    agent any
    stages {
        stage('Clone Code') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                // Ensure Minikube's Docker daemon is used so K8s can find the image
                sh 'eval $(minikube docker-env) && docker build -t myapp:latest .'
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
                sh 'kubectl apply -f k8s/service.yaml'
            }
        }
    }
}