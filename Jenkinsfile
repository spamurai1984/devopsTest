pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
	stage('Checkout Git') {
		steps { 
                    git branch: 'main', url: 'https://github.com/spamurai1984/devopsTest.git'
	 }
    }
        }
    }
}
