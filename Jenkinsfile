pipeline {
    agent any

    environment {
        // Define Docker image name and tag
        DOCKER_IMAGE = "helloworld:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ChanOoDev/HelloWorld.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image from HelloWorld folder
                    sh "docker build -t $DOCKER_IMAGE ./HelloWorld"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}