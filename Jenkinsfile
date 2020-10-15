pipeline {
    agent any
    stages {
        stage('Build') {
      steps {
        sh 'echo Run build...'
      }
        }
        stage('Test') {
      steps {
        sh 'echo Run tests...'
      }
        }
        stage('Stage') {
      steps {
        sh 'echo Deploy to Staging...'
      }
        }
        stage('Generate GATED change request') {
          steps {
        sh 'echo Creating change request'
        jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'in_progress',
                  enableGate: true,
                  serviceIds: ['<YOUR_SERVICE_ID>']
                )
          }
        }
        stage('Check gate') {
          steps {
            waitUntil {
              input message: 'Check for approval now?'
              checkGateStatus(
                site:'jsd-coin.atlassian.net',
                environmentId:'us-prod-1'
              )
            }
          }
        }
        stage('Production') {
      steps {
        sh 'echo Deploy to production...'
        jiraSendDeploymentInfo (
                  site: '<YOUR_SITE>.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'in_progress',
                  serviceIds: ['<YOUR_SERVICE_ID>']
                )
      }
      post {
        always {
          sh 'echo finished'
        }
        success {
          jiraSendDeploymentInfo (
                  site: '<YOUR_SITE>.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'successful',
                  serviceIds: ['<YOUR_SERVICE_ID>']
                )
        }
        failure {
          jiraSendDeploymentInfo (
                  site: '<YOUR_SITE>.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'failed',
                  serviceIds: ['<YOUR_SERVICE_ID>']
                )
        }
        aborted {
          jiraSendDeploymentInfo (
                  site: '<YOUR_SITE>.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'cancelled',
                  serviceIds: ['<YOUR_SERVICE_ID>']
                )
        }
      }
        }
    }
}
