pipeline {
  agent {
    kubernetes {
      label "node18"
      defaultContainer 'node:18-alpine'
    }
  }

  stages {
    stage('Test') {
      steps {
        container('node') {
          sh 'node --version'
        }
      }
    }
  }
}