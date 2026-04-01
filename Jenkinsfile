pipeline {
    agent any

    environment {
        IMAGE_NAME = "mostafa1006/my-app"
        DOCKER_CREDS = "docker-hub-creds"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/MostafaMohamed2001/jenkinstsk3.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDS) {
                        docker.image("${IMAGE_NAME}:${BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished 🔄"
        }
        success {
            echo "Image pushed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
