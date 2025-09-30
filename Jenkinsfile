pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the application using Maven/Gradle/NPM...'
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running tests using JUnit/TestNG/PyTest...'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Performing code analysis using SonarQube...'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Running security scan using Snyk/OWASP Dependency-Check...'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying application to staging using Docker/Kubernetes...'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests using Selenium/Postman...'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying application to production using Ansible/Terraform...'
                }
            }
        }
    }

    post {
        always {
            // Send email using Email Extension Plugin with build log attached
            emailext(
                subject: "Pipeline Notification: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                body: "The pipeline has completed.",
                to: 'vidhic1790@gmail.com',
                attachLog: true
            )
            echo 'Pipeline execution completed.'
        }
    }
}
