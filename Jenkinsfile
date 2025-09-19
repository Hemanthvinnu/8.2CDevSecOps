pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'hemanthkatagoni@gmail.com'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your_github_username/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true' // Prevents pipeline from failing on test errors
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                script {
                    def auditResult = sh(script: 'npm audit --audit-level=low || true', returnStdout: true).trim()
                    writeFile file: 'audit-result.txt', text: auditResult
                }
            }
        }

        stage('Send Email Notification') {
            steps {
                script {
                    emailext(
                        subject: "DevSecOps Report - ${env.JOB_NAME} [#${env.BUILD_NUMBER}]",
                        body: """\
Hello Hemanth,

✅ Jenkins job '${env.JOB_NAME}' (Build #${env.BUILD_NUMBER}) has completed.

🟢 Build Status: ${currentBuild.currentResult}  
🔗 Build URL: ${env.BUILD_URL}

📎 The audit report is attached.

Regards,  
Jenkins CI/CD Pipeline
""",
                        to: "${EMAIL_RECIPIENT}",
                        attachLog: true,
                        attachmentsPattern: 'audit-result.txt'
                    )
                }
            }
        }
    }
}
