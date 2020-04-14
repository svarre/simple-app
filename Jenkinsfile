#!/usr/bin/env groovy
pipeline {
  agent any
  stages {
    stage ('Build'){
      steps{
        script {
          def pom = readMavenPom file:'pom.xml'
          //def pomversion = pom.version
        }
        echo pom.version
        sh 'mvn clean install package'
        archiveArtifacts '**/*.war'
      }
      
    }
  }
}
