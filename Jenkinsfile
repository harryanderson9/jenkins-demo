pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }
        stage('staging') {
            steps {
                sh 'echo staging'
            }
        }
        stage('production') {
            steps {
                sh 'echo production'
            }
        }
    }
}