pipeline {
    agent any
    stages {
        stage("Test") {
            steps {
                git branch: 'main', url: 'https://github.com/harryanderson9/jenkins-demo.git'
                echo "Deploying to test"
            }
        }
        stage("Stage") {
            steps {
                echo "Deploying to staging"
            }
        }
        stage('Request approval') {
            steps {
                echo 'Raise change request...'
                jiraSendDeploymentInfo(site:'jsd-coin.atlassian.net',
                        environmentId:'us-prod-1',
                        environmentName:'us-prod-1',
                        environmentType:'production',
                        // now we can define a state of build explicitly
                        state:"pending",
                        enableGating:true,
                        serviceIds: ['b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC85NDRhNTUwOC0xMzVmLTExZWItYTFkMy0wYTc3ZjNmNDUzMDQ=']
                    )
            }
        }
        stage("Approval gate") {
            steps {
                waitUntil {
                input message: "Check for approval?"
                checkGatingStatus(site:'jsd-coin.atlassian.net', environmentId:'us-prod-1')
                }
            }
        }
        stage("Production") {
            steps {
                echo "Deploying to production!!"
            }
            post {
              always {
                sh 'sleep 2'
              }
              success {
                jiraSendDeploymentInfo (
                        site: 'jsd-coin.atlassian.net',
                        environmentId: 'us-prod-1',
                        environmentName: 'us-prod-1',
                        environmentType: 'production',
                        state: 'successful',
                        serviceIds: ['b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC85NDRhNTUwOC0xMzVmLTExZWItYTFkMy0wYTc3ZjNmNDUzMDQ=']
                      )
              }
            }
        }
    }
}