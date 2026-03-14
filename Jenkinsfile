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
                docker build -t orderservice:latest -f src/Production/Dockerfile src/Production
                """
            }
        }

        stage('Deploy') {
            steps {
                bat """
                echo Stopping old container if exists...
                docker stop orderservice
                docker rm orderservice
                echo Running new container...
                docker run -d --name orderservice -p 5001:8080 orderservice:latest
                """
            }
        }

    }
}