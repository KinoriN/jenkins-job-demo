def label = "slave-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'node18', image: 'node:18-alpine', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'docker', image: 'docker:latest', command: 'cat', ttyEnabled: true)
]) {
  node(label) {
    stage('checkout') {
      checkout scm
      sh 'cd jenkins-build-demo'
    }

    stage('build dist') {
      container('node18') {
        sh 'pnpm install --frozen-lockfile'
        sh 'pnpm build'
      }
    }
    
    post {
      success {
        sh 'tar -czvf dist.tar.gz dist'
        archiveArtifacts artifacts: 'dist.tar.gz', fingerprint: true
      }
    }
  }
}