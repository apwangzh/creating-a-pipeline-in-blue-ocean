pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('TEST') {
      environment {
        CI = 'true'
      }
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('deliv') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? '
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
}