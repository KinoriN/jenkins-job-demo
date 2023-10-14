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
        step('setup dependencies') {
          sh 'pnpm i'
        }
        step('build') {
          sh 'pnpm run build'
        }
      }
    }
  }
}