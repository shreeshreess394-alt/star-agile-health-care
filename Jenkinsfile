pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying WAR file to Tomcat...'
                deploy adapters: [
                    tomcat9(credentialsId: 'tomcat-creds', 
                    path: '', 
                    url: 'http://3.7.253.177:9090/')
                ], 
                contextPath: 'star-agile-health', 
                war: 'target/*.war'
            }
        }
    }
}
