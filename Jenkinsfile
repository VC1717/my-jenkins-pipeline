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
        echo 'Stage 1: Build - Build the code using a build automation tool to compile and package your code. You need to specify at least one build automation tool, e.g., Maven.'
      }
    }
    stage('Unit and Integration Tests') {
      steps {
        echo 'Stage 2: Unit and Integration Tests - Run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected. You need to specify test automation tools for this stage.'
      }
    }
    stage('Code Analysis') {
      steps {
        echo 'Stage 3: Code Analysis - Integrate a code analysis tool to analyse the code and ensure it meets industry standards. Research and select a tool to analyse your code using Jenkins'
      }
    }
    stage('Security Scan') {
      steps {
        echo 'Stage 4: Security Scan - Perform a security scan on the code using a tool to identify any vulnerabilities. Research and select a tool to scan your code.'
      }
    }
    stage('Deploy to Staging') {
      steps {
        echo 'Stage 5: Deploy to Staging - Deploy the application to a staging server (e.g., AWS EC2 instance).'
      }
    }
    stage('Integration Tests on Staging') {
      steps {
        echo 'Stage 6: Integration Tests on Staging - Run integration tests on the staging environment to ensure the application functions as expected in a production-like environment.'
      }
    }
    stage('Deploy to Production') {
      steps {
        echo 'Stage 7: Deploy to Production - Deploy the application to a production server (e.g., AWS EC2 instance).'
      }
    }


    post {
        success {
            emailext(
                to: 'vidhic1790@gmail.com',
                subject: "Pipeline Success - Build #${env.BUILD_NUMBER}",
                body: """
                Hello Team,

                The Jenkins pipeline has completed successfully.

                Regards,
                Jenkins Pipeline
                """,
                attachLog: true
            )
        }
        failure {
            emailext(
                to: 'vidhic1790@gmail.com',
                subject: "Pipeline Failed - Build #${env.BUILD_NUMBER}",
                body: """
                Hello Team,

                The Jenkins pipeline has failed. Please check Jenkins for details.

                Regards,
                Jenkins Pipeline
                """,
                attachLog: true
            )
        }

  }
}