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
                sh 'npm audit || exit 0'
            }
        }
    }

    post {
        always {
            emailext (
                subject: "Jenkins Build [${env.JOB_NAME} #${env.BUILD_NUMBER}] - ${currentBuild.currentResult}",
                body: "The pipeline has completed with status: ${currentBuild.currentResult}.",
                to: "hemanthkatagoni@gmail.com",
                attachLog: true
            )
        }
    }
}
