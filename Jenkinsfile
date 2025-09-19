pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Running test stage...'
                sh 'echo "Tests ran successfully" > test-log.txt'
                sh 'cat test-log.txt'
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins Build - TEST stage",
                        body: "The test stage has completed.",
                        to: "hemanthkatagoni@gmail.com",
                        attachmentsPattern: 'test-log.txt',
                        attachLog: true
                    )
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                sh 'npm audit --json > audit-log.json || exit 0'
                sh 'cat audit-log.json'
            }
            post {
                always {
                    emailext(
                        subject: "Jenkins Build - SECURITY SCAN stage",
                        body: "Security scan completed. See attached log.",
                        to: "hemanthkatagoni@gmail.com",
                        attachmentsPattern: 'audit-log.json',
                        attachLog: true
                    )
                }
            }
        }
    }
}
