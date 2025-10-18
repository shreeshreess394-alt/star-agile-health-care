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
                echo 'Building project using Maven...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Package and Deploy') {
            steps {
                echo 'Packaging application and deploying...'
            }
        }
    }
}
