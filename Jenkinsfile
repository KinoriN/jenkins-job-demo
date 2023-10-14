def label = "slave-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'node18', image: 'node:18-alpine', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'docker', image: 'docker:latest', command: 'cat', ttyEnabled: true)
]) {
  node(label) {
    stage('setup dependencies') {
      container('node18') {
        steps {
          step('checkout') {
            checkout scm
          }
          step('cd') {
            sh 'cd jenkins-build-demo'
          }
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
}