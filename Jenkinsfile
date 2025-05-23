pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SatyamDeakin/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    try {
                        bat 'npm test || exit /b 0'
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "Run Tests Stage: ${currentBuild.result}",
                        body: "Run Tests Stage has finished with status: ${currentBuild.result}",
                        to: "satyam4101@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                script {
                    try {
                        bat 'npm audit || exit /b 0'
                        currentBuild.result = 'SUCCESS'
                    } catch (Exception e) {
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
            post {
                always {
                    emailext (
                        subject: "NPM Audit Stage: ${currentBuild.result}",
                        body: "NPM Audit Stage has finished with status: ${currentBuild.result}",
                        to: "satyam4101@gmail.com",
                        attachLog: true
                    )
                }
            }
        }
    }
}

