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
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh './venv/bin/pytest test_app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Deploy') {
            steps {
                // Example: running Docker container
                sh '''
                docker stop my-python-app || true
                docker rm my-python-app || true
                docker run -d -p 5000:5000 --name my-python-app $DOCKER_IMAGE
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

