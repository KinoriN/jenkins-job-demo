def label = "slave-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'node18', image: 'node:18-alpine', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'docker', image: 'docker:latest', command: 'cat', ttyEnabled: true)
]) {
  node(label) {
    stage('Get a nodejs') {
      container('node18') {
        sh 'ls'
        // sh 'pnpm i'
        // sh 'pnpm run build'
      }
    }
  }
}