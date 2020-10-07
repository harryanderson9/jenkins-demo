pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo building...'
            }
        }
        stage('Test') {
            steps {
                sh 'echo building...'
            }
        }
        stage('Staging') {
            steps {
                sh 'echo staging'
            }
        }
        stage('Production') {
            steps {
                sh 'echo production'
            }
            post {
              always {
                jiraSendDeploymentInfo site: 'jsd-coin.atlassian.net', environmentId: 'us-prod-1', environmentName: 'us-prod-1', environmentType: 'production', serviceIds: ['b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC85NzYyMzcyYS0wODNjLTExZWItYjJjMC0wYTc3ZjNmNDUzMDQ=']
              }
            }
        }
    }
}