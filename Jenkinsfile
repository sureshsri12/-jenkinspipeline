pipeline {
    agent any
    stages {
        stage('Build front-end') {
            steps {
                sh 'cd client && npm install && npm start && npm run build'
            }
        }
        stage('Build back-end') {
            steps {
                sh 'service2 && mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
