pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'  // Install dependencies using npm
            }
        }
        stage('Test') {
            steps {
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "chmod +x ./jenkins/scripts/test.sh && ./jenkins/scripts/test.sh"'  // Run test.sh with bash
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/deliver-for-development.sh"'
                input message: 'Finished using the web site? (Click "Proceed" to continue)', timeout: 300, timeoutMessage: 'Timeout reached'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/kill.sh"'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/deploy-for-production.sh"'
                input message: 'Finished using the web site? (Click "Proceed" to continue)', timeout: 300, timeoutMessage: 'Timeout reached'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/kill.sh"'
            }
        }
    }
}
