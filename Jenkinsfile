pipeline {
  agent {
    docker {
      image 'node:18-alpine'
    }

  }
  stages {
    stage('log') {
      steps {
        sh 'echo "test"'
      }
    }

  }
}