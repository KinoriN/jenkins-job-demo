def label = "slave-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'node18', image: 'node:18-alpine', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'docker', image: 'docker:latest', command: 'cat', ttyEnabled: true)
]) {
  node(label) {
    stage('checkout') {
      checkout scm
      stash name: 'artifacts-code', includes: "jenkins-build-demo/**"
    }

    stage('build dist') {
      container('node18') {
        unstash 'artifacts-code'

        sh 'npm i pnpm -g'
        sh 'pnpm install --frozen-lockfile'
        sh 'pnpm build'

        stash name: 'artifacts-dist', includes: "dist/**"
      }
    }

    stage('build docker image') {
      container('docker') {
        unstash 'artifacts-dist'
      }
    }
  }
}