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
                sh 'docker login nexus.kugal.online:8083 -u jenkins --password-stdin < ./pass'
                sh 'docker tag myapp:v1 nexus.kugal.online:8083/myapp_nodejs'
                sh 'docker push nexus.kugal.online:8083/myapp_nodejs'
            }
        }
        stage('Pull') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    sshagent(['jenkins']) {
                        sh 'ssh -o StrictHostKeyChecking=no root@5.42.74.179 uptime'
                        sh 'ssh -v root@5.42.74.179 "docker stop nodeJSxxx && docker container rm nodeJSxxx"'
                        sh 'ssh -v root@5.42.74.179 "docker login 77.91.86.201:8083 -u jenkins --password-stdin < ./pass && docker pull 77.91.86.201:8083/myapp_nodejs && docker run -it --name nodeJSxxx --detach -p 3000:3000 77.91.86.201:8083/myapp_nodejs:latest"'
                    }
                }
            }
        }
    }
}
    
