pipeline {
    agent any
    
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
                credentialsId: '876c9019-4110-4da2-9245-5f34830c9105'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Проверяем доступность Docker
                    sh 'docker --version'
                    
                    // Собираем образ
                    docker.build("my-app:${env.BUILD_ID}")
                }
            }
        }
    }
}
