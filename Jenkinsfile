pipeline {
    agent any
    stages {
        // a new way how to use the plugin
        stage('Deploy - testing') {
            steps {
                echo 'Queueing...'
                jiraSendDeploymentInfo(site:'jsd-coin.atlassian.net',
                        environmentId:'us-prod-1',
                        environmentName:'us-prod-1',
                        environmentType:'production',
                        // now we can define a state of build explicitly
                        state:"pending",
                        enableGating:true,
                        serviceIds: [
                "b:YXJpOmNsb3VkOmdyYXBoOjpzZXJ2aWNlLzA4MjY0MTE2LWQ1MzEtMTFlYS1iYWVhLTEyOGI0MjgxOTQyNC8wZmI5Mjc4ZS0xMjZlLTExZWItYWEzNS0wYTc3ZjNmNDUzMDQ="]
                    )
            }
        }
        stage("check gate") {
            steps {
                waitUntil {
                    input message: "Check for approval?"
                    checkGatingStatus(site:'jsd-coin.atlassian.net', environmentId:'us-tst-1')
                }
            }
        }
        stage("deploy") {
            steps {
                echo "Deploying!"
            }
        }
    }
}
