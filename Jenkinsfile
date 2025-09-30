pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from GitHub"
                git branch: 'main', url: 'https://github.com/VC1717/my-jenkins-pipeline.git'
                echo "Compiling the code and generating artifacts."
                echo "Build successful with Maven"
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests started and completed"
                echo "Running integration tests started and completed"
                echo "Unit and integration test successfully completed using JUnit"
            }
            post {
                success {
                    mail to: 'vidhic1790@gmail.com',
                        subject: 'Hello Buddy? (Unit & Integration Tests Success)',
                        body: 'Bhai ki Body'
                }
                failure {
                    mail to: 'vidhic1790@gmail.com',
                        subject: 'Hello Buddy? (Unit & Integration Tests Failed)',
                        body: 'Bhai ki Body failed'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Running Code Analysis started and completed"
                echo "Code analysis done using FindBugs"
            }
        }

        stage('Security Scan') {
            steps {
                echo "Running Security Scan started and completed"
                echo "Security Scan done using Nessus"
            }
            post {
                success {
                    mail to: 'vidhic1790@gmail.com',
                        subject: 'Security Scan Success',
                        body: 'The Security Scan has succeeded. Find attached logs for more information.'
                }
                failure {
                    mail to: 'vidhic1790@gmail.com',
                        subject: 'Security Scan Failed',
                        body: 'The Security Scan has failed. Find attached logs for more information.'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Running Deploy to Staging started and completed"
                echo "Deploy to staging completed using Jenkins Deploy Plugin"
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running Integration Tests on Staging started and completed"
                echo "Tests successful using JUnits"
            }
            post {
                success {
                    mail to: 'vidhic1790@gmail.com',
                        subject: 'Integration Tests on Staging Success',
                        body: 'The Integration Tests on Staging have succeeded. Find attached logs for more information.'
                }
                failure {
                    mail to: 'vidhic1790@gmail.com',
                        subject: 'Integration Tests on Staging Failed',
                        body: 'The Integration Tests on Staging have failed. Find attached logs for more information.'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Running Deploy to Production started and completed"
                echo "Production successfully completed using Jenkins Deploy Plugin"
            }
        }
    }
}
