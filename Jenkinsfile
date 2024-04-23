pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS = credentials('Docker-Credentials')
    }
    stages {
        stage('Build and Push Docker Images') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'Docker-Credentials') {
                        def apps = ['uc1', 'uc2', 'uc3', 'frontend']
                        for (app in apps) {
                            def image = docker.build("bhuvan02/${app}:latest", "./${app}")
                            image.push()
                        }
                    }
                }
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
