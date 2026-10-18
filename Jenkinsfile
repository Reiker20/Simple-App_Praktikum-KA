pipeline {
    agent any
    environment {
        IMAGE_NAME = 'reikaelvaretta/simple-app' // Sesuaikan dengan username Docker Hub Anda jika berbeda
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
    }
    stages {
        stage('Checkout') { 
            steps { 
                checkout scm 
            } 
        }
        stage('Build') { 
            steps { 
                bat 'echo "Mulai build aplikasi di Windows"' 
            } 
        }
       stage('Build Docker Image') {
            steps {
                bat '"C:\\Program Files\\Docker\\Docker\\resources\\bin\\docker.exe" build -t reikaelvaretta/simple-app:9 .'
            }
        }
        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: REGISTRY_CREDENTIALS, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    bat 'docker login -u %USER% -p %PASS%'
                    bat "docker push %IMAGE_NAME%:%BUILD_NUMBER%"
                    bat "docker tag %IMAGE_NAME%:%BUILD_NUMBER% %IMAGE_NAME%:latest"
                    bat "docker push %IMAGE_NAME%:latest"
                }
            }
        }
    }
    post { 
        always { 
            echo 'Selesai build' 
        } 
    }
}
