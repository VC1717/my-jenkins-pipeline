pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', 
                    credentialsId: 'vidhic1790@gmail.com', 
                    url: 'https://github.com/VC1717/my-jenkins-pipeline.git'
            }
        }

        stage('Stage 1: Build') {
            steps {
                echo 'Stage 1: Build - Installing required dependencies and building the application using tools such as Maven, Gradle, NPM, Webpack, or Vite.'
            }
        }

        stage('Stage 2: Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Unit and Integration Tests - Executing tests using tools like JUnit or NUnit.'
            }
            post {
                success {
                    emailext attachLog: true, 
                        body: "Stage 2: Unit and Integration Tests passed successfully.", 
                        subject: "Pipeline Notification: Stage 2 Passed", 
                        to: "vidhic1790@gmail.com"
                }
                failure {
                    emailext attachLog: true, 
                        body: "Stage 2: Unit and Integration Tests failed. Please check the logs for details.", 
                        subject: "Pipeline Notification: Stage 2 Failed", 
                        to: "vidhic1790@gmail.com"
                }
            }
        }

        stage('Stage 3: Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Integrate code analysis tools like ESLint or SonarQube to ensure the React code meets industry standards and best practices.'
            }
        }

        stage('Stage 4: Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Perform a security scan on the React application using tools like OWASP ZAP or other scanners to identify potential vulnerabilities.'
            }
            post {
                success {
                    emailext attachLog: true, 
                        body: "Stage 4: Security Scan passed successfully.", 
                        subject: "Pipeline Notification: Stage 4 Passed", 
                        to: "vidhic1790@gmail.com"
                }
                failure {
                    emailext attachLog: true, 
                        body: "Stage 4: Security Scan failed. Please check the logs for details.", 
                        subject: "Pipeline Notification: Stage 4 Failed", 
                        to: "vidhic1790@gmail.com"
                }
            }
        }

        stage('Stage 5: Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploy the React application to a staging environment (e.g., AWS S3, Netlify) for testing and preview.'
            }
        }

        stage('Stage 6: Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Integration Tests on Staging - Run integration tests on the staged React application using tools like Cypress or Selenium to ensure it functions as expected in a production-like environment.'
            }
        }

        stage('Stage 7: Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploy the React application to the production environment (e.g., AWS S3, Netlify, or a web server).'
            }
        }
    }
}
