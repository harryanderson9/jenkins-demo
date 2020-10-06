pipeline {
    agent { docker { image 'maven:3.3.3' } }
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