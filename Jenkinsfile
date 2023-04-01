pipeline {
    agent any
    stages {
        stage('Build front-end') {
            steps {
                sh '/home/tlspc-087/my-app-docker/client && npm install && npm run build'
            }
        }
        stage('Build back-end') {
            steps {
                sh '/home/tlspc-087/my-app-docker/service2 && mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
