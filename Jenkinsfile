pipeline {
    agent any
    //  environment {
    //     ACR_SERVER = 'your-acr-server.azurecr.io'
    //     ACR_USERNAME = credentials('acr-username')
    //     ACR_PASSWORD = credentials('acr-password')
    //     DOCKER_IMAGE_NAME = 'your-docker-image-name'
    //     DOCKERFILE_PATH = 'path/to/Dockerfile'
    // }
	
stages{
  //  stage('Build Docker image') {
  //           steps {
  //               sh "docker build -t ${DOCKER_IMAGE_NAME} ${DOCKERFILE_PATH}"
  //           }
  //       }
  //       stage('Push to ACR') {
  //           steps {
  //               withCredentials([usernamePassword(credentialsId: 'acr-credentials-id', usernameVariable: 'ACR_USERNAME', passwordVariable: 'ACR_PASSWORD')]) {
  //                   azurePushImage(
  //                       azureCredentialsId: 'azure-credentials-id',
  //                       resourceGroup: 'your-resource-group',
  //                       registry: "${ACR_SERVER}",
  //                       imageName: "${DOCKER_IMAGE_NAME}",
  //                       imageTag: "${BUILD_NUMBER}",
  //                       force: true
  //                   )
  //               }
  //           }
  //       }
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
                sh 'docker-compose up --build'
            }
        }
    }
}

