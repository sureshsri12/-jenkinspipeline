pipeline {
    agent any
    stages {
      // stage('sonarqube analysis'){
      //   // def scannerHome = tool 'sonarqube';
      //   // withSonarQubeEnv("sonarqube"){
      //   //     sh "${scannerHome}/bin/sonar-scanner \
      //   //     -D sonar.login=admin \
      //   //     -D sonar.password=admin@123 \
      //   //     -D sonar.projectKey= Fullstackproject\
      //   //     -D sonar.exclusions=vendor/**,resources/**.**/*.java \
      //   //     -D sonar.host.url=http://localhost:9000/"
      //   sh 'sonar-scanner'
    
      stage("verify tooling") {
      steps {
        sh '''
          docker version
          docker info
          docker compose version 
          curl --version
        '''
      }
    }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}

