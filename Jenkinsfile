pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/shreyap-gif/security-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                mvn clean package -DskipTests
                '''
            }
        }

        stage('Security Scan - Dependency Check') {
            steps {
                sh '''
                mvn org.owasp:dependency-check-maven:check
                '''
            }
        }

        stage('Publish Reports') {
            steps {
                publishHTML([
                    reportDir: 'target/dependency-check-report',
                    reportFiles: 'dependency-check-report.html',
                    reportName: 'OWASP Security Report'
                ])
            }
        }
    }
}
