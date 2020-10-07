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
        stage('Request change approval') {
          steps {
                sh 'echo requesting change approval'
                jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net', 
                  environmentId: 'us-prod-1', 
                  environmentName: 'us-prod-1', 
                  environmentType: 'production', 
                  state: "pending",
                  enableGate: true,
                  serviceIds: [
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC85NzYyMzcyYS0wODNjLTExZWItYjJjMC0wYTc3ZjNmNDUzMDQ=', 
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC9jZWU1NThlYS0wODQ1LTExZWItYWNhMC0wYTc3ZjNmNDUzMDQ='
                  ]
                )
        }
        state("Check gate") {
          steps {
            waitUntil {
              input message: "Check for approval?"
              checkGateStatus(site:'dhurin.jira-dev.com', environmentId:'us-tst-1')
            }
          }
        }
        stage('Production') {
            steps {
                sh 'echo start production deploy'
                jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net', 
                  environmentId: 'us-prod-1', 
                  environmentName: 'us-prod-1', 
                  environmentType: 'production', 
                  state: "in_progress",
                  serviceIds: [
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC85NzYyMzcyYS0wODNjLTExZWItYjJjMC0wYTc3ZjNmNDUzMDQ=', 
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC9jZWU1NThlYS0wODQ1LTExZWItYWNhMC0wYTc3ZjNmNDUzMDQ='
                  ]
                )
                sh 'echo production deploy finished'
            }
            post {
              always {
                sh 'echo finished'
              }
              success {
                jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net', 
                  environmentId: 'us-prod-1', 
                  environmentName: 'us-prod-1', 
                  environmentType: 'production', 
                  state: 'successful',
                  serviceIds: [
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC85NzYyMzcyYS0wODNjLTExZWItYjJjMC0wYTc3ZjNmNDUzMDQ=', 
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC9jZWU1NThlYS0wODQ1LTExZWItYWNhMC0wYTc3ZjNmNDUzMDQ='
                  ]
                )
              }
              failure {
                jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net', 
                  environmentId: 'us-prod-1', 
                  environmentName: 'us-prod-1', 
                  environmentType: 'production', 
                  state: 'failed',
                  serviceIds: [
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC85NzYyMzcyYS0wODNjLTExZWItYjJjMC0wYTc3ZjNmNDUzMDQ=', 
                    'b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC9jZWU1NThlYS0wODQ1LTExZWItYWNhMC0wYTc3ZjNmNDUzMDQ='
                  ]
                )
              }
            }
        }
    }
}