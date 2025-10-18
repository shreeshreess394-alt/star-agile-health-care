pipeline {
    agent any

    environment {
        // Name of your Docker image
        IMAGE_NAME = "medicure-app"
    }

    stages {
        stage('Git Checkout') {
            steps {
                echo "Pulling latest code from GitHub..."
                checkout scm
            }
        }

        stage('Build with Maven') {
            steps {
                echo "Building project using Maven..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'sudo docker build -t ${IMAGE_NAME}:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                echo "Stopping old container (if running)..."
                sh '''
                CONTAINER_ID=$(sudo docker ps -q --filter ancestor=${IMAGE_NAME}:latest)
                if [ ! -z "$CONTAINER_ID" ]; then
                    sudo docker stop $CONTAINER_ID
                    sudo docker rm $CONTAINER_ID
                fi
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running new container on port 9090..."
                sh 'sudo docker run -d -p 9090:8080 ${IMAGE_NAME}:latest'
            }
        }

        stage('Verify Container') {
            steps {
                echo "Listing all running containers..."
                sh 'sudo docker ps'
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful!"
        }
        failure {
            echo "❌ Deployment failed. Check console output."
        }
    }
}
