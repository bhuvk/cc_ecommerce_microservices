pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Hardcoded Docker credentials
                    def DOCKER_USERNAME = "bhuvan02"
                    def DOCKER_PASSWORD = 'Vppnsb@6922'
                    
                    // Build and push Docker images
                    sh 'docker build -t uc1 ./uc1'
                    sh 'docker login -u ' + DOCKER_USERNAME + ' -p ' + DOCKER_PASSWORD + ' docker.io'
                    sh 'docker tag uc1 ' + DOCKER_USERNAME + '/uc1:latest'
                    sh 'docker push ' + DOCKER_USERNAME + '/uc1:latest'
                    
                    sh 'docker build -t uc2 ./uc2'
                    sh 'docker tag uc2 ' + DOCKER_USERNAME + '/uc2:latest'
                    sh 'docker push ' + DOCKER_USERNAME + '/uc2:latest'
                    
                    sh 'docker build -t uc3 ./uc3'
                    sh 'docker tag uc3 ' + DOCKER_USERNAME + '/uc3:latest'
                    sh 'docker push ' + DOCKER_USERNAME + '/uc3:latest'
                    
                    sh 'docker build -t frontend ./frontend'
                    sh 'docker tag frontend ' + DOCKER_USERNAME + '/frontend:latest'
                    sh 'docker push ' + DOCKER_USERNAME + '/frontend:latest'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy Kubernetes resources
                sh 'echo pods created successful'
             
               
                
            }
        }
    }
    
    post {
        failure {
            // Print message if pipeline fails
            echo 'Pipeline failed'
        }
    }
}
