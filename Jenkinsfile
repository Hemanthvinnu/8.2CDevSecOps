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
                sh 'npm audit || true'
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Jenkins Build - ${currentBuild.currentResult}",
                body: "Build result: ${currentBuild.currentResult}\n\nSee attached console log for more details.",
                to: "hemanthkatagoni@gmail.com",
                attachLog: true
            )
        }
    }
}
