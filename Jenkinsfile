pipeline {
    agent any
    environment {
        IMAGE_NAME = 'nishdoc18/node-sample'
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/nishanth1897/node-js-sample.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}")
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}

