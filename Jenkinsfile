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
                echo 'Stage 2: Run unit and integration tests.'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Perform code analysis.'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security scan for vulnerabilities.'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to staging.'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Run integration tests on staging.'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to production.'
            }
        }
    }

    post {
        success {
            emailext (
                subject: "Build #${env.BUILD_NUMBER} SUCCESS",
                body: "The pipeline finished successfully. Check console logs attached.",
                to: 'vidhic1790@gmail.com',
                attachLog: true
            )
        }
        failure {
            emailext (
                subject: "Build #${env.BUILD_NUMBER} FAILED",
                body: "The pipeline failed. Please check the attached logs.",
                to: 'vidhic1790@gmail.com',
                attachLog: true
            )
        }
    }
}
