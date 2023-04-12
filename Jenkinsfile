pipeline {
    agent any
	// environment {
	//               PATH = "$PATH:/usr/share/maven-3.6.0/bin"
	// 			  }
  //   stages {
  //            stage('Build') {
	// 		 steps{
	// 		         sh 'mvn clean package'
	// 		 }
	// 		} 

//       stage('SonarQube analysis') {
//     steps {
//         withSonarQubeEnv('Fullstackproject') {
//             sh 'mvn sonar:sonar'
//         }
//     }
// }
stages{
stage('SonarQube analysis') {
  steps {
    withSonarQubeEnv('SonarQube') {
      sh "sonar-scanner -Dsonar.projectKey=Fullstackproject -Dsonar.projectName='Fullstackproject' -Dsonar.sources=src"
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

