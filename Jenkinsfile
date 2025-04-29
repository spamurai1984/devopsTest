pipeline {

    agent any
    
    environment {
        DOCKER_IMAGE = "my-react-app"
        DOCKER_TAG = "${env.BUILD_ID}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:spamurai1984/devopsTest.git'
           }
        }
        
        stage('Build and Deploy') {
            steps {
                script {
                    // Собираем Docker-образ (включая сборку React через многостадийную сборку)
                    docker.build("${env.DOCKER_IMAGE}:${env.DOCKER_TAG}")
                    
                    // Останавливаем старый контейнер
                    sh 'docker stop react-container || true'
                    sh 'docker rm react-container || true'
                    
                    // Запускаем новый контейнер
                    sh "docker run -d -p 80:80 --name react-container ${env.DOCKER_IMAGE}:${env.DOCKER_TAG}"
                }
            }
        }
    }
}
