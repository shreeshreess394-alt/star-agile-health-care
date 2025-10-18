pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Shriraksha384/star-agile-health-care.git',
                    credentialsId: 'github-token'
            }
        }

        stage('Build using Maven') {
            steps {
                echo "Building project using Maven..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo "Building Docker image..."
                sh 'sudo docker build -t medicure-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "Running Docker container..."
                sh 'sudo docker run -d -p 8080:8082 medicure-app'
            }
        }

        stage('Verify Container') {
            steps {
                echo "Checking running containers..."
                sh 'sudo docker ps'
            }
        }
    }
}
