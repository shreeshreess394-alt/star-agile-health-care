pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/shreeshreess394-alt/star-agile-health-care.git',
                    credentialsId: 'github-token'
            }
        }

        stage('Build using Maven') {
            steps {
                echo "Building project using Maven..."
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running unit tests..."
                sh 'mvn test'
            }
        }
    }
}
