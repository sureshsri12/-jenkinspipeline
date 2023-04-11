pipeline {
    agent any
  
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
      tools {
        maven 'Maven 3.8.4' // specify the Maven installation
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install' // run Maven command
            }
        }
    }
      stage('SonarQube analysis') {
    steps {
        withSonarQubeEnv('Fullstackproject') {
            sh 'mvn sonar:sonar'
        }
    }
}
    
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


