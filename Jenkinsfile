pipeline {
    agent any

    environment {
        IMAGE_NAME = "it-tools-custom"
        CONTAINER_NAME = "my-it-tools"
        PORT = "8082"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/polojunarendra-svg/IT-tools_Depolyment-using_DevOps.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                    docker run -d --name $CONTAINER_NAME --network devops-network -p $PORT:80 $IMAGE_NAME:latest
                '''
            }
        }
    }

    post {
        success {
            echo "IT-Tools deployed successfully at http://localhost:8082"
        }
        failure {
            echo "Deployment failed. Check the console output above."
        }
    }
}