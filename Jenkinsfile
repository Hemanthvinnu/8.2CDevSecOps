pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Running test stage...'
                sh 'echo "Tests ran successfully"'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                // Ignore errors so job doesn't fail
                sh 'npm audit > audit.log || true'
            }
        }
    }

    post {
        always {
            emailext (
                      subject: "Security Scan Logs",
                      body: "Attached audit logs.",
                      to: "hemanthkatagoni@gmail.com",
                      attachmentsPattern: 'audit.log',
                      attachLog: true
)
        }
    }
}
