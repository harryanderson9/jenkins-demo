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
        // stage('Generate GATED change request') {
        //   steps {
        //         sh 'echo Creating change request'
        //         jiraSendDeploymentInfo (
        //           site: 'jsd-coin.atlassian.net',
        //           environmentId: 'us-prod-1',
        //           environmentName: 'us-prod-1',
        //           environmentType: 'production',
        //           state: "in_progress",
        //           enableGate: true,
        //           serviceIds: ['<YOUR_SERVICE_ID>']
        //         )
        //   }
        // }
        // stage("Check gate") {
        //   steps {
        //     waitUntil {
        //       input message: "Check for approval now?"
        //       checkGateStatus(
        //         site:'jsd-coin.atlassian.net',
        //         environmentId:'us-prod-1'
        //       )
        //     }
        //   }
        // }
        stage('Production') {
      steps {
        sh 'echo Deploy to production...'
        jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'in_progress',
                  serviceIds: ['b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC8wZmI5Mjc4ZS0xMjZlLTExZWItYWEzNS0wYTc3ZjNmNDUzMDQ=']
                )
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
                  serviceIds: ['b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC8wZmI5Mjc4ZS0xMjZlLTExZWItYWEzNS0wYTc3ZjNmNDUzMDQ=']
                )
        }
        failure {
          jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'failed',
                  serviceIds: ['b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC8wZmI5Mjc4ZS0xMjZlLTExZWItYWEzNS0wYTc3ZjNmNDUzMDQ=']
                )
        }
        aborted {
          jiraSendDeploymentInfo (
                  site: 'jsd-coin.atlassian.net',
                  environmentId: 'us-prod-1',
                  environmentName: 'us-prod-1',
                  environmentType: 'production',
                  state: 'cancelled',
                  serviceIds: ['b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC8wZmI5Mjc4ZS0xMjZlLTExZWItYWEzNS0wYTc3ZjNmNDUzMDQ=']
                )
        }
      }
        }
    }
}
