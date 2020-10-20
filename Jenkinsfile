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
        stage('Production') {
          steps {
            jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'in_progress',
                )
            sh 'echo Deploy to production...'
          }
          post {
              always {
                sh 'sleep 2'
                sh 'echo finished'
              }
              success {
                jiraSendDeploymentInfo (
                        site: 'jsd-coin.atlassian.net',
                        environmentId: 'us-prod-1',
                        environmentName: 'us-prod-1',
                        environmentType: 'production',
                        state: 'successful',
                      )
              }
              failure {
                jiraSendDeploymentInfo (
                        site: 'jsd-coin.atlassian.net',
                        environmentId: 'us-prod-1',
                        environmentName: 'us-prod-1',
                        environmentType: 'production',
                        state: 'failed',
                      )
              }
              aborted {
                jiraSendDeploymentInfo (
                        site: 'jsd-coin.atlassian.net',
                        environmentId: 'us-prod-1',
                        environmentName: 'us-prod-1',
                        environmentType: 'production',
                        state: 'cancelled',
                      )
              }
            }
          }
        }
    }
}
