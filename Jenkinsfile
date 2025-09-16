pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/VC1717/8.2CDevSecOps.git'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }
    stage('Run Tests') {
      steps {
        sh 'npm test || true'
      }
      post {
        always {
          emailext body: 'Status: $BUILD_STATUS', subject: 'Run Tests Stage - $BUILD_STATUS', to: 'vidhic1790@gmail.com', attachLog: true
        }
      }
    }
    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }
    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
      post {
        always {
          emailext body: 'Status: $BUILD_STATUS', subject: 'NPM Audit Stage - $BUILD_STATUS', to: 'vidhic1790@gmail.com', attachLog: true
        }
      }
    }
  }
}