pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/santanu879/order-svc.git'
            }
        }

        stage('Docker Build') {
            steps {
                bat """
                echo Building Docker image...
                docker build -t orderservice:latest .
                """
            }
        }

        stage('Deploy') {
            steps {
                bat """
                echo Running Docker container...
                docker stop orderservice || exit 0
                docker rm orderservice || exit 0
                docker run -d --name orderservice -p 5001:8080 orderservice:latest
                """
            }
        }

    }
}