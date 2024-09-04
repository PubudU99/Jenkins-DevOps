pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/PubudU99/Jenkins-DevOps'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                sh 'docker build -t pubudu123/nodeapp-cuban:$BUILD_NUMBER .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'DockerPassword', variable: 'DockerPswd')]) {
                    script {
                        sh "docker login -u pubudu123 -p $DockerPswd"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker push pubudu123/nodeapp-cuban:$BUILD_NUMBER'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}