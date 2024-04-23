pipeline {
    agent any
    environment {
        // Utilizing Jenkins-managed credentials by their ID
        DOCKER_CREDENTIALS = credentials('8a17736e-c9b3-4258-976e-c9a93c167f4f')
    }
    stages {
        stage('Build and Push Docker Images') {
            steps {
                // Build Docker images from respective directories
                sh 'docker build -t bhuvan02/uc1:latest ./uc1'
                sh 'docker build -t bhuvan02/uc2:latest ./uc2'
                sh 'docker build -t bhuvan02/uc3:latest ./uc3'
                sh 'docker build -t bhuvan02/frontend:latest ./frontend'

                // Directly use hardcoded credentials for Docker Hub login
                sh 'echo "Vppnsb@6922" | docker login -u "bhuvan02" --password-stdin https://index.docker.io/v1/'

                // Push Docker images to Docker Hub
                sh 'docker push bhuvan02/uc1:latest'
                sh 'docker push bhuvan02/uc2:latest'
                sh 'docker push bhuvan02/uc3:latest'
                sh 'docker push bhuvan02/frontend:latest'
            }
        }
       
        stage('Deploy') {
            steps {
                // Apply Kubernetes configurations
                sh 'kubectl apply -f kubernetes.yaml'
            }
        }
    }
   
    post {
        failure {
            // Post action for failed pipeline
            echo 'Pipeline failed'
        }
    }
}
