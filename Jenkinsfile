pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'echo "Build log example" > build.log'
            }
        }
    }
    post {
        always {
            // Send email with log attachment
            emailext(
                subject: "${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                body: "Please find the build log attached.",
                recipientProviders: [[$class: 'DevelopersRecipientProvider']], // optional: for trigger-based recipients
                to: 'vidhic1790@gmail.com',
                attachLog: true
            )
        }
    }
}
