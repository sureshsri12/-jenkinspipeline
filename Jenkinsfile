pipeline {
    agent any
    stages {
        // stage('Build front-end') {
        //     steps {
        //         sh 'cd client && npm i && npm install && npm start && npm run build'
        //     }
        // }
        // stage('Build back-end') {
        //     steps {
        //         sh 'cd service1 && npm start && npm start && npm run build'
        //     }
        // }
    stage("verify tooling") {
      steps {
        sh '''
          docker version
          docker info
          docker compose version 
          curl --version
          jq --version
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

// pipeline {
//   agent any
  
//   stages {
//     stage('Build and run containers') {
//       steps {
//         sh 'docker-compose up -d'
//       }
//     }
    
//     // Other stages and steps for your pipeline
//   }
  
//   post {
//     always {
//       // Stop and remove the containers
//       sh 'docker-compose down'
//     }
//   }
// }