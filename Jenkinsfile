pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "chanoodev/helloworld:latest"
        DOCKERHUB_CREDENTIALS = "dockerhub-pat" // Jenkins credentials ID
    }
	
	triggers {
        githubPush() // Trigger pipeline on GitHub push
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
                    sh 'docker build -t $DOCKER_IMAGE ./HelloWorld'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKERHUB_CREDENTIALS}", usernameVariable: 'USERNAME', passwordVariable: 'TOKEN')]) {
                    // Use triple single quotes to avoid interpolating sensitive data in Groovy
                    sh '''echo "$TOKEN" | docker login -u "$USERNAME" --password-stdin'''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}