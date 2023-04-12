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
    withSonarQubeEnv(installationName: 'sonarqube') {
      // sh "sonar-scanner -Dsonar.projectKey=Fullstackproject -Dsonar.projectName='Fullstackproject' -Dsonar.sources=src"
      sh "sonar-scanner -Dsonar.host.url=http://localhost:9000/ -Dsonar.login=sqp_c51a2eaf72d11e08b824fbf793cb53096f609866 -Dsonar.projectKey=Fullstackproject"
    }
  }
}
 stage("Quality Gate") {
    steps {
        timeout(time: 2, unit: 'MINUTES') {
		   waitForQualityGate abortPipeline: true
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

