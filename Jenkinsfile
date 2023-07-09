pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Build Docker image
                sh 'docker build -t myapp:v1 .'
            }
        }
    }
}
