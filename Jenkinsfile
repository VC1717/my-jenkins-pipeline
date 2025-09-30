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
        success {
            script {
                emailext(
                    subject: "SUCCESS: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                    body: """
                        <h2>Pipeline Execution Successful</h2>
                        <p><strong>Job:</strong> ${JOB_NAME}</p>
                        <p><strong>Build Number:</strong> ${BUILD_NUMBER}</p>
                        <p><strong>Build Status:</strong> SUCCESS</p>
                        <p><strong>Build URL:</strong> <a href="${BUILD_URL}">${BUILD_URL}</a></p>
                        <hr>
                        <p>All stages completed successfully. Console log is attached.</p>
                    """,
                    to: 'vidhic1790@gmail.com',
                    mimeType: 'text/html',
                    attachLog: true,
                    compressLog: true,
                    attachmentsPattern: '*/.log'
                )
            }
        }
        
        failure {
            script {
                emailext(
                    subject: "FAILURE: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                    body: """
                        <h2>Pipeline Execution Failed</h2>
                        <p><strong>Job:</strong> ${JOB_NAME}</p>
                        <p><strong>Build Number:</strong> ${BUILD_NUMBER}</p>
                        <p><strong>Build Status:</strong> FAILURE</p>
                        <p><strong>Build URL:</strong> <a href="${BUILD_URL}">${BUILD_URL}</a></p>
                        <hr>
                        <p style="color: red;">The pipeline has failed. Console log is attached.</p>
                    """,
                    to: 'vidhic1790@gmail.com',
                    mimeType: 'text/html',
                    attachLog: true,
                    compressLog: true,
                    attachmentsPattern: '*/.log'
                )
            }
        }
        
        always {
            script {
                emailext(
                    subject: "NOTIFICATION: ${JOB_NAME} - Build #${BUILD_NUMBER} - ${currentBuild.result}",
                    body: """
                        <h2>Pipeline Notification</h2>
                        <p><strong>Job:</strong> ${JOB_NAME}</p>
                        <p><strong>Build Number:</strong> ${BUILD_NUMBER}</p>
                        <p><strong>Build Status:</strong> ${currentBuild.result}</p>
                        <p><strong>Build URL:</strong> <a href="${BUILD_URL}">${BUILD_URL}</a></p>
                        <hr>
                        <p>The pipeline has completed. Console log is attached.</p>
                    """,
                    to: 'vidhic1790@gmail.com',
                    mimeType: 'text/html',
                    attachLog: true,
                    compressLog: true,
                    attachmentsPattern: '*/.log'
                )
            }
        }
    }
}
