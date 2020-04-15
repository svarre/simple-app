pipeline{
  agent any 
  stages {
    stage ('artifact_create') {
      steps {
        sh 'mvn clean install'
        archive '**/*.war'
      }
    }
  }
}
