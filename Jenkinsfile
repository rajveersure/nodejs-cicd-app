pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nodejs-app'
        CONTAINER_PORT = '3000'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Node.js dependencies...'
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Stopping any existing container...'
                sh "docker rm -f ${IMAGE_NAME} || true"
                
                echo 'Running Docker container...'
                sh "docker run -d -p ${CONTAINER_PORT}:${CONTAINER_PORT} --name ${IMAGE_NAME} ${IMAGE_NAME}"
            }
        }

        stage('Test Deployment') {
            steps {
                echo "App should now be running on port ${CONTAINER_PORT}"
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}