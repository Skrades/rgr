pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "my-app-image:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                // Клонируем репозиторий
                git branch: 'main', url: 'https://github.com/username/repository.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Сборка Docker-образа
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Deploy Container') {
            steps {
                // Остановка и запуск нового контейнера
                sh '''
                docker stop my-app || true
                docker rm my-app || true
                docker run -d --name my-app -p 8080:8080 $DOCKER_IMAGE
                '''
            }
        }
    }
}
