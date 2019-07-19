pipeline {
  agent none
  stages {
    stage('Build 6') {
      parallel {
        stage('Build') {
          agent {
            docker {
              image 'node:6-alpine'
              args '-p 3000:3000'
            }

          }
          steps {
            sh 'npm install'
          }
        }
        stage('Build 8') {
          agent {
            docker {
              image 'node:8-alpine'
              args '-p 3001:3000'
            }

          }
          steps {
            sh 'npm install'
          }
        }
      }
    }
    stage('Test') {
      agent any
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }
    stage('Deliver') {
      agent any
      steps {
        sh './jenkins/scripts/deliver.sh'
        input 'Finished using the web site? (Click "Proceed" to continue) '
        sh './jenkins/scripts/kill.sh'
      }
    }
    stage('Clear') {
      agent any
      steps {
        sh './jenkins/scripts/kill.sh'
      }
    }
  }
  environment {
    CI = 'true'
  }
}