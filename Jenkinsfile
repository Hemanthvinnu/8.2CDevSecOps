pipeline {
    agent any

    environment {
        NODE_ENV = 'development'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/Hemanthvinnu/8.2CDevSecOps.git'
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
                    sh 'npm audit --audit-level=low || true'
                    writeFile file: 'audit-result.txt', text: readFile('audit-result.txt')
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
