pipeline {

    agent any

    environment {
        IMAGE_NAME = "react-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('react-app') {
                    sh 'docker build -t $IMAGE_NAME .'
                }
            }
        }

        stage('Remove Old Container') {
            steps {
                sh 'docker rm -f react-container || true'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker run -d \
                --name react-container \
                -p 3000:80 \
                react-app
                '''
            }
        }
    }
}
