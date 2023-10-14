def label = "slave-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'node18', image: 'node:18-alpine', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'docker', image: 'docker:latest', command: 'cat', ttyEnabled: true)
]) {
  node(label) {
    stage('checkout') {
      checkout scm
    }

    stage('build dist') {
      container('node18') {
        sh 'npm config set registry http://npm.dev:4873/'
        sh 'npm i pnpm -g'
        sh 'cd jenkins-build-demo && pnpm install --frozen-lockfile'
        sh 'cd jenkins-build-demo && pnpm build'
      }
    }

    stage('build docker image') {
      container('docker') {
        sh 'docker build -t jenkins-build-demo:latest jenkins-build-demo'
      }
    }
  }
}