pipeline {
    agent any

    stages {
        stage('Pre-Build Check') {
            steps {
                echo 'Auto-trigger test: Build activated by new commit.'
            }
        }

        stage('Build') {
            steps {
                echo 'Stage 1: Build - Build the code using Maven.'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Run unit tests to ensure the code functions as expected and run integration tests to ensure the different components of the application work together as expected.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Integrate a code analysis tool to analyse the code and ensure it meets industry standards.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Perform a security scan on the code using a tool to identify any vulnerabilities.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploy the application to a staging server.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Run integration tests on the staging environment.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploy the application to a production server.'
            }
        }
    }

    post {
        always {
            // Send email with Jenkins console log attached
            emailext (
                subject: "Build #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                body: "The pipeline finished with status: ${currentBuild.currentResult}. The Jenkins build log is attached.",
                to: 'vidhic1790@gmail.com',
                attachLog: true
            )
        }
    }
}
