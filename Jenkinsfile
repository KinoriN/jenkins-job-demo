def label = "slave-${UUID.randomUUID()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'node18', image: 'node:18-alpine', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'docker', image: 'docker:dind', command: 'cat', ttyEnabled: true)
], volumes: [
  hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
]) {
  node(label) {
    stage('checkout') {
      checkout scm
    }

    stage('build dist') {
      container('node18') {
        sh 'npm set registry http://npm:4873/'
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
