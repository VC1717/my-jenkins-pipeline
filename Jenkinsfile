pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
    post {
        always {
            emailext(
                subject: "${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: "Build finished. Please find attached log.",
                to: 'vidhic1790@gmail.com',
                attachLog: true,
                mimeType: 'text/html'
                // leave 'from' empty to use system SMTP credentials
            )
        }
    }
}
