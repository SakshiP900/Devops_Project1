pipeline {
    agent any

    environment {
        APP_NAME = "my-java-app"
        DOCKER_IMAGE = "my-java-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SakshiP900/Devops_Project1.git'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-java-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                docker stop my-java-app || true
                docker rm my-java-app || true
                docker run -d -p 5000:5000 --name my-java-app %DOCKER_IMAGE%
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline finished"
        }
    }
}

