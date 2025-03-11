pipeline {
    agent any
    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/kpkm25/flask-ci-cd.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t prabsin/flask-ci-cd:latest .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-creds', url: '']) {
                    sh 'docker push prabsin/flask-ci-cd:latest'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}
