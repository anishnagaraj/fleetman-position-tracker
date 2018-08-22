def label = "mypod-${UUID.randomUUID().toString()}"
podTemplate(label: label, containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat')
  ]) {

    node(label) {
        stage('Preparation') {
            git 'https://github.com/anishnagaraj/fleetman-position-tracker'
        }
        container('maven') {
                stage('Build') {
                    sh 'mvn package'
                }
        }
        stage('Results') {
            junit '**/target/surefire-reports/TEST-*.xml'
            archive 'target/*.jar'
        }
        
    }
}
