pipeline {
    agent any
    
    // Добавляем настройки окружения для Docker
    environment {
        DOCKER_HUB = credentials('docker-hub-credentials') // Если нужен доступ к Docker Hub
    }
    
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
        
        stage('Checkout Git') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/spamurai1984/devopsTest.git',
                credentialsId: '876c9019-4110-4da2-9245-5f34830c9105' // Ваш credentialsId из лога
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Проверяем, что Docker установлен и доступен
                    sh 'docker --version'
                    
                    // Собираем образ (замените на ваш Dockerfile)
                    docker.build("my-app:${env.BUILD_ID}")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    // Останавливаем и удаляем старый контейнер
                    sh 'docker stop my-app-container || true'
                    sh 'docker rm my-app-container || true'
                    
                    // Запускаем новый контейнер
                    sh "docker run -d --name my-app-container my-app:${env.BUILD_ID}"
                }
            }
        }
    }
}
