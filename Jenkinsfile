pipeline {
    agent any

    environment {
        IMAGE_NAME = "mostafa1006/my-app"
        DOCKER_CREDS = "docker-hub-creds"
    }

    stages {

        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/MostafaMohamed2001/jenkinstsk3.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest", ".")
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDS) {
                        docker.image("${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Image pushed to your Docker Hub ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
