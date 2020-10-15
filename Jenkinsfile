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
        sh 'echo Deploy to Production...'
      }
      post {
        always {
          sh 'echo finished'
        }
      }
    }
    }
}
