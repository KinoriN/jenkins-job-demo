def label = "slave-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'node18', image: 'node:18-alpine')
]) {
  node(label) {
    stage('Get a nodejs') {
      container('node18') {
        sh 'node --version'
      }
    }
  }
}