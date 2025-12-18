pipeline {
    agent any

    environment {
        APP_NAME = "my-python-app"
        DOCKER_IMAGE = "my-python-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SakshiP900/Devops_Project1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m venv venv'
                bat '.\\venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                bat '.\\venv\\Scripts\\pytest test_app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t my-python-app:latest .'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                docker stop my-python-app || exit 0
                docker rm my-python-app || exit 0
                docker run -d -p 5000:5000 --name my-python-app %DOCKER_IMAGE%
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
