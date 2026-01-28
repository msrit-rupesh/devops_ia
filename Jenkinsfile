pipeline {
    agent any
    environment {
        DOCKERHUB_CRED = credentials('dockerhub')
        IMAGE_NAME = "rupeshmsrit//devops_ia"
    }

    stages {
        stage('checkout') {
            steps { git url: 'https://github.com/msrit-rupesh/devops_ia/', branch: 'main' }
        }
        stage('Build Docker Image') {
            steps {
                script { dockerImage = docker.build("${IMAGE_NAME}:latest") }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
                        dockerImage.push()
                    }
                }
            }
        }
    }
    post {
        success { echo "Pipeline Successful" }
        failure { echo "Pipeline Failed" }
        always { deleteDir() }
    }
}




