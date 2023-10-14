pipeline {
  agent {
    docker {
      image 'node:18-alpine'
    }

  }
  stages {
    stage('error') {
      steps {
        sh 'echo "test"'
      }
    }

  }
}