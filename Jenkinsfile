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
                git branch: 'main', url: 'https://github.com/spamurai1984/devopsTest.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("my-app:${env.BUILD_ID}")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker stop my-app-container || true'
                    sh 'docker rm my-app-container || true'
                    
                    docker.run(
                        "my-app:${env.BUILD_ID}",
                        "--name my-app-container -d"
                    )
                }
            }
        }
    }
}
