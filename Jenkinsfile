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
         steps {
                // Pull Docker image to private regestry Nexus
                sh 'docker login 79.137.248.252:8083 -u jenkins --password-stdin < ./pass'
                sh 'docker tag myapp:v1 79.137.248.252:8083/myapp_nodejs'
                sh 'docker push 79.137.248.252:8083/myapp_nodejs'
            }
        }
    }
}
