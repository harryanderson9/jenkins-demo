pipeline {
    agent { docker { image 'node:6.3' } }
    stages {
        stage('Build') {
            steps {
                sh 'npm --version'
            }
        }
        stage('Deploy to staging') {
            steps {
                sh 'echo Deploying to Staging...'
            }
        }
        stage('Deploy to production') {
            steps {
                sh 'echo Deploying to production...'
            }
        }
    }
}