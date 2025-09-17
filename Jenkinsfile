pipeline {
    agent any

    stages {

        stage('Pre-Build Check') {
            steps {
                echo 'Stage 0: Pre-Build Check - Triggered by commit.'
            }
        }

        stage('Build') {
            steps {
                echo 'Stage 1: Build - Using Maven to compile and package code.'
                // Example: sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Stage 2: Running Unit and Integration Tests with JUnit.'
                // Example: sh 'mvn test'
            }
            post {
                always {
                    emailext(
                        to: 'vidhic1790@gmail.com',
                        subject: "Unit & Integration Tests Stage - ${currentBuild.currentResult}",
                        body: """
                        Hello Team,

                        The *Unit & Integration Tests* stage has finished with status: ${currentBuild.currentResult}.
                        Please find the logs attached.

                        Regards,
                        Jenkins Pipeline
                        """,
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Stage 3: Code Analysis - Using SonarQube to analyze code quality.'
                // Example: sh 'mvn sonar:sonar'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Stage 4: Security Scan - Using OWASP Dependency-Check to detect vulnerabilities.'
                // Example: sh 'dependency-check.sh --scan . --format XML'
            }
            post {
                always {
                    emailext(
                        to: 'vidhic1790@gmail.com',
                        subject: "Security Scan Stage - ${currentBuild.currentResult}",
                        body: """
                        Hello Team,

                        The *Security Scan* stage has finished with status: ${currentBuild.currentResult}.
                        Please find the logs attached.

                        Regards,
                        Jenkins Pipeline
                        """,
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Stage 5: Deploy to Staging - Deploying to AWS EC2.'
                // Example: sh 'scp target/app.jar ec2-user@staging-server:/app/'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Stage 6: Running integration tests on Staging environment using Selenium.'
                // Example: sh 'mvn verify -Pstaging'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Stage 7: Deploy to Production - Deploying to AWS EC2.'
                // Example: sh 'scp target/app.jar ec2-user@prod-server:/app/'
            }
        }
    }

    post {
        success {
            emailext(
                to: 'vidhic1790@gmail.com',
                subject: "Pipeline Success - Build #${env.BUILD_NUMBER}",
                body: """
                Hello Team,

                ✅ The Jenkins pipeline has completed successfully.

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

                ❌ The Jenkins pipeline has failed. Please check Jenkins for details.

                Regards,
                Jenkins Pipeline
                """,
                attachLog: true
            )
        }
    }
}
