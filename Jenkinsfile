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
                // Pull Docker image 
                sshagent(['jenkins_privat']) {
                sh 'ssh -o StrictHostKeyChecking=no root@5.42.74.179 uptime'
                sh 'ssh -v root@5.42.74.179 "docker stop $(docker ps -aq) && docker container rm nodeJSxxx"'
                sh 'ssh -v root@5.42.74.179 "docker login 79.137.248.252:8083 -u jenkins --password-stdin < ./pass && docker pull 79.137.248.252:8083/myapp_nodejs && docker run -it --name nodeJSxxx --detach -p 3000:3000 79.137.248.252:8083/myapp_nodejs:latest"'
                }
            }
        }
    }
}
    
