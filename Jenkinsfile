pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = credentials('Docker-Credentials')
    }
    stages {
        stage('Build') {
            steps {
                bat 'docker build -t uc1 ./uc1'
                bat 'docker login -u ${bhuvan02} -p ${Vppnsb@6922} ${https://index.docker.io/v1/}'
                bat 'docker tag uc1 bhuvan02/uc1:latest'
                bat 'docker push bhuvan02/uc1:latest'
                bat 'docker build -t uc2 ./uc2'
                bat 'docker tag uc1 bhuvan02/uc2:latest'
                bat 'docker push bhuvan02/uc2:latest'
                bat 'docker build -t uc3 ./uc3'
                bat 'docker tag uc3 bhuvan02/uc3:latest'
                bat 'docker push bhuvan02/uc3:latest'
                bat 'docker build -t frontend ./frontend'
                bat 'docker tag frontend bhuvan02/frontend:latest'
            }
        }
        
        stage('Deploy') {
            steps {
                 bat 'kubectl apply -f kubernetes.yaml'
            }
        }
    }
    
    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
