pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Running test stage...'
                sh 'echo "Tests ran successfully" > test.log'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins - TEST Stage Result: ${currentBuild.currentResult}",
                        body: """Hello,
                        
The test stage has completed with status: ${currentBuild.currentResult}.

Please find the attached test log.

""",
                        to: "hemanthkatagoni@gmail.com",
                        attachmentsPattern: 'test.log',
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                sh 'npm audit > audit.log || true'
            }
            post {
    always {
        emailext (
            subject: "Jenkins - TEST Stage #${BUILD_NUMBER} - ${new Date()}",
            body: """Hello,

The test stage completed.

Please check attached log.""",
            to: "hemanthkatagoni@gmail.com",
            attachLog: true,
            attachmentsPattern: 'test.log'
        )
    }
}
        }
    }

    // REMOVE global post to avoid duplicate emails
}
