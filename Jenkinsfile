pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t myimage:latest .'
        sh 'docker-compose build'
        sh 'docker-compose run web npm run build'
      }
    }
    stage('Tests') {
      steps {
        "Unit Tests": {
          sh 'docker-compose run --name test --rm web npm run test'
        }
      }
    }

    stage('Deploy to Staging') {
      when {
        expression { env.BRANCH_NAME == 'master' }
      }
      steps {
        echo 'todo: deploy to staging'
      }
    }

    stage('Create feature environment') {
      when {
        expression { env.BRANCH_NAME != 'master' }
      }

      steps {
        echo 'todo: create custom environment'
      }
    }
  }
}

// node {
//   try {
//     stage('Checkout') {
//       checkout scm
//     }
//     stage('Environment') {
//       sh 'git --version'
//       echo "Branch: ${env.BRANCH_NAME}"
//       sh 'docker -v'
//       sh 'printenv'
//     }
//     stage('Build Docker test'){
//       sh 'docker build -t react-test -f Dockerfile.test --no-cache . '
//     }
//     stage('Docker test'){
//       sh 'docker run --rm react-test'
//     }
//     stage('Clean Docker test'){
//       sh 'docker rmi react-test'
//     }
//     stage('Deploy'){
//       if (env.BRANCH_NAME == 'master') {
//         sh 'docker build -t react-app --no-cache .'
//         sh 'docker tag react-app localhost:5000/react-app'
//         sh 'docker push localhost:5000/react-app'
//         sh 'docker rmi -f react-app localhost:5000/react-app'
//       }
//     }
//   }
//   catch (err) {
//     throw err
//   }
// }
