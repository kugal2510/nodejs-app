pipeline {
    agent any

    environment {
        DOCKER_HOST = 'tcp://79.137.248.25:8083'
    }

    stages {
        stage('Build') {
            steps {
                // Checkout source code from your version control system
                checkout scm
                // Build Docker image
                sh 'docker build -t myapp:v1 .'
            }
        }
        stage('Push') {
            steps {
                // Push Docker image to private regestry Nexus
                sh 'docker login 79.137.248.252:8083 -u jenkins --password-stdin < ./pass'
                sh 'docker tag myapp:v1 79.137.248.252:8083/myapp_nodejs'
                sh 'docker push 79.137.248.252:8083/myapp_nodejs'
            }
        }
        stage('Pull') {
            steps {
                options {
                sshagent(credentials: ['jenkins'])
                disableStrictHostKeyChecking(true)
                }
                // Pull Docker image 
                sh 'ssh root@5.42.74.179'
                sh 'docker login 79.137.248.252:8083 -u jenkins --password-stdin < ./pass'
                sh 'docker pull 79.137.248.252:8083/myapp_nodejs'
                sh 'docker run -it --detach -p 3000:3000 79.137.248.252:8083/myapp_nodejs:latest'
            }
        }
    }
}
