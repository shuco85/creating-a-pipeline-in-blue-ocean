pipeline {
  agent any
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
      }
    }
    stage('Message add') {
      agent any
      steps {
        input '-Finished using the web site? (Click "Proceed" to continue) '
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