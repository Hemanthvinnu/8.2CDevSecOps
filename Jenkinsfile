pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                script {
                    // Save audit result to file
                    sh 'npm audit --audit-level=low > audit-result.txt || true'
                }
            }
        }

        stage('Send Email Notification') {
            steps {
                script {
                    emailext(
                        subject: "DevSecOps Jenkins Pipeline Completed",
                        body: "Hello Team,\n\nThe Jenkins pipeline has completed successfully. See attached audit result.\n\nRegards,\nJenkins",
                        to: "hemanthkatagoni@gmail.com",
                        attachLog: true,
                        attachmentsPattern: 'audit-result.txt'
                    )
                }
            }
        }
    }
}
