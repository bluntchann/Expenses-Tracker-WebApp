
pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "expensetracker"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/sneh-create/Expenses-Tracker-WebApp.git'
            }
        }

        stage('Clean Previous Containers') {
            steps {
                echo 'Stopping and removing old containers...'
                sh 'docker compose down || true'
            }
        }

        stage('Start Application using Docker Compose') {
            steps {
                echo 'Starting app and MySQL with Docker Compose...'
                sh 'docker compose up -d'
            }
        }

        stage('Verify Running Containers') {
            steps {
                echo 'Checking running containers...'
                sh 'docker ps'
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed. Cleaning up...'
            sh 'docker compose down || true'
        }
        success {
            echo '✅ Build succeeded. App should be live on port 8081!'
        }
    }
}
