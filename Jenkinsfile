pipeline {
    agent any 
   
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/NilmiKaushallya/4044-Lakshani'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t lakshani4044/my-assignment:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'assignment-4044', variable: 'assignment')]) {
               bat'docker login -u lakshani4044 -p ${assignment}'
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push lakshani4044/my-assignment:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}