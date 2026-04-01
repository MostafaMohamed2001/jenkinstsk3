pipeline {
    agent any

    environment {
        IMAGE_NAME = "mostafa1006/my-app"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/MostafaMohamed2001/jenkinstsk3.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh """
                docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .
                docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest
                """
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-hub-creds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh "echo \"$PASS\" | docker login -u \"$USER\" --password-stdin"
                }
            }
        }

        stage('Push Image') {
            steps {
                sh """
                docker push ${IMAGE_NAME}:${BUILD_NUMBER}
                docker push ${IMAGE_NAME}:latest
                """
            }
        }
    }

    post {
        always {
            echo "Pipeline finished 🔄"
            sh "docker system prune -f || true"
        }
        success {
            echo "Image pushed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
