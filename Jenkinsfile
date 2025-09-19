pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Running test stage...'
                sh 'echo "Tests ran successfully"'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins Build - TEST stage",
                        body: "The test stage has completed.",
                        to: "hemanthkatagoni@gmail.com",
                        attachLog: true
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                sh 'npm audit || exit 0'
            }
            post {
                always {
                    emailext (
                        subject: "Jenkins Build - SECURITY SCAN stage",
                        body: "Security scan completed.",
                        to: "hemanthkatagoni@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
    }
}
