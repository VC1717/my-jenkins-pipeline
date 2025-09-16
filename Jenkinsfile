pipeline {
  agent any
  stages {

    stage('Pre-Build Check') {
      steps {
        echo 'Auto-trigger test: Build #6 activated by new commit.'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Unit and Integration Tests') {
      steps {
        echo 'Stage 2: Unit and Integration Tests - Run unit tests here.'
      }
    }

    stage('Code Analysis') {
      steps {
        echo 'Stage 3: Code Analysis - Run code analysis tool here.'
      }
    }

    stage('Security Scan') {
      steps {
        echo 'Stage 4: Security Scan - Run security scan tool here.'
      }
    }

    stage('Deploy to Staging') {
      steps {
        echo 'Stage 5: Deploy to Staging - Deploy application to staging.'
      }
    }

    stage('Integration Tests on Staging') {
      steps {
        echo 'Stage 6: Integration Tests on Staging - Run integration tests in staging.'
      }
    }

    stage('Deploy to Production') {
      steps {
        echo 'Stage 7: Deploy to Production - Deploy application to production.'
      }
    }
  }

  post {
    success {
      mail to: 'vidhic1790@gmail.com',
           subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
           body: "The pipeline completed successfully!"
    }
    failure {
      mail to: 'vidhic1790@gmail.com',
           subject: "FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
           body: "The pipeline failed!"
    }
  }
}
