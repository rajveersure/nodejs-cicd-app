pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t nodejs-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f nodejs-container || true'
                sh 'docker run -d -p 80:3000 --name nodejs-container nodejs-app'
            }
        }
    }
}
