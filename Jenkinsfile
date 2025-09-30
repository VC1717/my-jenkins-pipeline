pipeline {
    agent any
    
    tools {
        maven 'Maven-3.9.0' // Configure this name in Jenkins Global Tool Configuration
        jdk 'JDK-17' // Configure this name in Jenkins Global Tool Configuration
    }
    
    environment {
        STAGING_SERVER = 'ec2-user@staging-server-ip'
        PRODUCTION_SERVER = 'ec2-user@production-server-ip'
        EMAIL_RECIPIENT = 'vidhic1790@gmail.com'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                echo 'Checking out code from GitHub repository...'
                git branch: 'main', 
                    credentialsId: 'github-credentials', 
                    url: 'https://github.com/VC1717/my-jenkins-pipeline.git'
                echo 'Code checkout completed successfully'
            }
        }
        
        stage('Build') {
            steps {
                echo '========================================='
                echo 'Stage 1: Build'
                echo '========================================='
                echo 'Building the application using Maven...'
                echo 'Tool: Apache Maven'
                echo 'Description: Compiling source code and packaging into JAR/WAR files'
                
                script {
                    // Actual Maven build commands
                    sh 'mvn clean compile'
                    sh 'mvn package -DskipTests'
                }
                
                echo 'Build completed successfully'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo '========================================='
                echo 'Stage 2: Unit and Integration Tests'
                echo '========================================='
                echo 'Running unit tests and integration tests...'
                echo 'Tools: JUnit 5, Mockito, TestNG'
                echo 'Description: Executing automated tests to verify code functionality'
                
                script {
                    // Run unit tests using Maven
                    sh 'mvn test'
                    
                    // Run integration tests
                    sh 'mvn verify -P integration-tests'
                }
                
                echo 'All tests completed successfully'
            }
            post {
                always {
                    // Publish test results
                    junit '*/target/surefire-reports/.xml'
                    
                    emailext(
                        subject: "Test Stage Notification: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                        body: """
                            <h2>Unit and Integration Tests Completed</h2>
                            <p><strong>Job:</strong> ${JOB_NAME}</p>
                            <p><strong>Build Number:</strong> ${BUILD_NUMBER}</p>
                            <p><strong>Stage:</strong> Unit and Integration Tests</p>
                            <p><strong>Status:</strong> ${currentBuild.currentResult}</p>
                            <p><strong>Build URL:</strong> <a href="${BUILD_URL}">${BUILD_URL}</a></p>
                            <hr>
                            <p>Test execution completed. Please review the attached console log for detailed results.</p>
                        """,
                        to: "${EMAIL_RECIPIENT}",
                        mimeType: 'text/html',
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo '========================================='
                echo 'Stage 3: Code Analysis'
                echo '========================================='
                echo 'Performing static code analysis...'
                echo 'Tool: SonarQube'
                echo 'Description: Analyzing code quality, detecting bugs, code smells, and security vulnerabilities'
                
                script {
                    // SonarQube analysis
                    withSonarQubeEnv('SonarQube-Server') {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=my-jenkins-pipeline -Dsonar.host.url=http://localhost:9000'
                    }
                    
                    // Wait for Quality Gate
                    timeout(time: 5, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
                }
                
                echo 'Code analysis completed successfully'
            }
        }
        
        stage('Security Scan') {
            steps {
                echo '========================================='
                echo 'Stage 4: Security Scan'
                echo '========================================='
                echo 'Performing security vulnerability scan...'
                echo 'Tools: OWASP Dependency-Check, Snyk'
                echo 'Description: Scanning for security vulnerabilities in dependencies and code'
                
                script {
                    // OWASP Dependency Check
                    sh 'mvn org.owasp:dependency-check-maven:check'
                    
                    // Alternative: Snyk security scan
                    // sh 'snyk test --all-projects'
                }
                
                echo 'Security scan completed successfully'
            }
            post {
                always {
                    // Publish security scan results
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
                    
                    emailext(
                        subject: "Security Scan Notification: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                        body: """
                            <h2>Security Scan Completed</h2>
                            <p><strong>Job:</strong> ${JOB_NAME}</p>
                            <p><strong>Build Number:</strong> ${BUILD_NUMBER}</p>
                            <p><strong>Stage:</strong> Security Scan</p>
                            <p><strong>Status:</strong> ${currentBuild.currentResult}</p>
                            <p><strong>Build URL:</strong> <a href="${BUILD_URL}">${BUILD_URL}</a></p>
                            <hr>
                            <p>Security scan completed. Please review the attached console log for vulnerability report.</p>
                        """,
                        to: "${EMAIL_RECIPIENT}",
                        mimeType: 'text/html',
                        attachLog: true,
                        compressLog: true
                    )
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo '========================================='
                echo 'Stage 5: Deploy to Staging'
                echo '========================================='
                echo 'Deploying application to staging environment...'
                echo 'Tools: Docker, AWS CLI, SCP'
                echo 'Description: Deploying packaged application to AWS EC2 staging server'
                
                script {
                    // Copy artifact to staging server
                    sh """
                        scp -o StrictHostKeyChecking=no target/*.war ${STAGING_SERVER}:/opt/applications/
                    """
                    
                    // Restart application on staging server
                    sh """
                        ssh -o StrictHostKeyChecking=no ${STAGING_SERVER} 'sudo systemctl restart tomcat'
                    """
                    
                    // Alternative: Docker deployment
                    // sh 'docker build -t my-app:staging .'
                    // sh 'docker push my-app:staging'
                    // sh 'ssh ${STAGING_SERVER} "docker pull my-app:staging && docker-compose up -d"'
                }
                
                echo 'Deployment to staging completed successfully'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo '========================================='
                echo 'Stage 6: Integration Tests on Staging'
                echo '========================================='
                echo 'Running integration tests on staging environment...'
                echo 'Tools: Selenium WebDriver, Postman/Newman, REST Assured'
                echo 'Description: Testing application functionality in production-like staging environment'
                
                script {
                    // Run API integration tests
                    sh 'mvn verify -P staging-integration-tests -Dtest.url=http://staging-server-ip:8080'
                    
                    // Alternative: Run Postman collections
                    // sh 'newman run postman-collection.json -e staging-environment.json'
                    
                    // Alternative: Run Selenium tests
                    // sh 'mvn test -Dtest=StagingE2ETests -Dselenium.url=http://staging-server-ip:8080'
                }
                
                echo 'Staging integration tests completed successfully'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo '========================================='
                echo 'Stage 7: Deploy to Production'
                echo '========================================='
                echo 'Deploying application to production environment...'
                echo 'Tools: AWS CLI, Ansible, Terraform, Docker'
                echo 'Description: Deploying verified application to AWS EC2 production server'
                
                script {
                    // Manual approval before production deployment
                    input message: 'Deploy to Production?', ok: 'Deploy'
                    
                    // Copy artifact to production server
                    sh """
                        scp -o StrictHostKeyChecking=no target/*.war ${PRODUCTION_SERVER}:/opt/applications/
                    """
                    
                    // Restart application on production server
                    sh """
                        ssh -o StrictHostKeyChecking=no ${PRODUCTION_SERVER} 'sudo systemctl restart tomcat'
                    """
                    
                    // Alternative: Ansible deployment
                    // sh 'ansible-playbook -i inventory/production deploy.yml'
                    
                    // Alternative: Terraform deployment
                    // sh 'terraform apply -auto-approve -var-file=production.tfvars'
                }
                
                echo 'Deployment to production completed successfully'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
            emailext(
                subject: "SUCCESS: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                body: """
                    <h2>Pipeline Execution Successful</h2>
                    <p><strong>Job:</strong> ${JOB_NAME}</p>
                    <p><strong>Build Number:</strong> ${BUILD_NUMBER}</p>
                    <p><strong>Status:</strong> SUCCESS</p>
                    <p><strong>Build URL:</strong> <a href="${BUILD_URL}">${BUILD_URL}</a></p>
                    <p><strong>Duration:</strong> ${currentBuild.durationString}</p>
                    <hr>
                    <h3>Completed Stages:</h3>
                    <ul>
                        <li>Build</li>
                        <li>Unit and Integration Tests</li>
                        <li>Code Analysis</li>
                        <li>Security Scan</li>
                        <li>Deploy to Staging</li>
                        <li>Integration Tests on Staging</li>
                        <li>Deploy to Production</li>
                    </ul>
                    <p>All stages completed successfully. Application is now live in production.</p>
                """,
                to: "${EMAIL_RECIPIENT}",
                mimeType: 'text/html',
                attachLog: true,
                compressLog: true
            )
        }
        
        failure {
            echo 'Pipeline failed!'
            emailext(
                subject: "FAILURE: ${JOB_NAME} - Build #${BUILD_NUMBER}",
                body: """
                    <h2>Pipeline Execution Failed</h2>
                    <p><strong>Job:</strong> ${JOB_NAME}</p>
                    <p><strong>Build Number:</strong> ${BUILD_NUMBER}</p>
                    <p><strong>Status:</strong> FAILURE</p>
                    <p><strong>Build URL:</strong> <a href="${BUILD_URL}">${BUILD_URL}</a></p>
                    <p><strong>Duration:</strong> ${currentBuild.durationString}</p>
                    <hr>
                    <p style="color: red;">The pipeline has failed. Please check the attached console log for error details.</p>
                """,
                to: "${EMAIL_RECIPIENT}",
                mimeType: 'text/html',
                attachLog: true,
                compressLog: true
            )
        }
        
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
    }
}
