pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Checkout source code from your version control system
                checkout scm
                // Build Docker image
                sh 'docker build -t myapp:v1 .'
            }
        }
    }
}
