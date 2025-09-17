pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/VC1717/8.2CDevSecOps.git'
            }
        }
        
        stage('Debug - Check Files') {
            steps {
                sh '''
                echo "Current directory:"
                pwd
                echo "Files in current directory:"
                ls -la
                echo "Checking for package.json:"
                ls -la package.json || echo "package.json not found"
                '''
            }
        }
        
        stage('Setup Environment') {
            steps {
                sh '''
                # Check if npm exists, if not install it
                if ! command -v npm &> /dev/null; then
                    echo "npm not found, installing Node.js and npm..."
                    apt update
                    apt install -y curl
                    curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
                    apt install -y nodejs
                fi
                node --version
                npm --version
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'npm test || true' // Allows pipeline to continue despite test failures
            }
            post {
                always {
                    // Email notification after test stage
                    emailext (
                        subject: "Jenkins Pipeline - Test Stage ${currentBuild.currentResult}: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                        body: """
                        <h2>Test Stage Completed</h2>
                        <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                        <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                        <p><strong>Status:</strong> ${currentBuild.currentResult}</p>
                        <p><strong>Build URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                        <p><strong>Stage:</strong> Run Tests</p>
                        <p>Please find the build logs attached.</p>
                        """,
                        mimeType: 'text/html',
                        to: 'vidhic1790@gmail.com',
                        attachLog: true,
                        compressLog: true,
                        replyTo: 'vidhic1790@gmail.com'
                    )
                }
            }
        }
        
        stage('Generate Coverage Report') {
            steps {
                // Ensure coverage report exists
                sh 'npm run coverage || true'
            }
        }
        
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true' // This will show known CVEs in the output
            }
            post {
                always {
                    // Email notification after security scan stage
                    emailext (
                        subject: "Jenkins Pipeline - Security Scan ${currentBuild.currentResult}: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                        body: """
                        <h2>Security Scan Stage Completed</h2>
                        <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                        <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                        <p><strong>Status:</strong> ${currentBuild.currentResult}</p>
                        <p><strong>Build URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                        <p><strong>Stage:</strong> NPM Audit (Security Scan)</p>
                        <p>The security scan has been completed. Please review the attached logs for any vulnerabilities found.</p>
                        """,
                        mimeType: 'text/html',
                        to: 'vidhic1790@gmail.com',
                        attachLog: true,
                        compressLog: true,
                        replyTo: 'vidhic1790@gmail.com'
                    )
                }
            }
        }
    }
    
    post {
        always {
            // Final pipeline notification
            emailext (
                subject: "Jenkins Pipeline ${currentBuild.currentResult}: ${env.JOB_NAME} - ${env.BUILD_NUMBER}",
                body: """
                <h2>Pipeline Execution Complete</h2>
                <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                <p><strong>Build Number:</strong> ${env.BUILD_NUMBER}</p>
                <p><strong>Final Status:</strong> ${currentBuild.currentResult}</p>
                <p><strong>Build URL:</strong> <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>
                <p><strong>Duration:</strong> ${currentBuild.durationString}</p>
                <p>The complete pipeline has finished execution. Please find the full build logs attached.</p>
                """,
                mimeType: 'text/html',
                to: 'vidhic1790@gmail.com',
                attachLog: true,
                compressLog: true,
                replyTo: 'vidhic1790@gmail.com'
            )
        }
    }
}