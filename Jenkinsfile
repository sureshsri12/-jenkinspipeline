pipeline {
    agent any
      tools { 
        maven 'Maven 3.3.9' 
        jdk 'jdk8' 
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${/opt/apache-maven-3.6.3}"
                    echo "M2_HOME = ${/opt/apache-maven-3.6.3}"
                ''' 
            }
        }
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
}

