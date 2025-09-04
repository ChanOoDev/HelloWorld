pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ChanOoDev/HelloWorld.git'
            }
        }
        
      
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}
