#!/usr/bin/env groovy
pipeline{
  agent any
  environment {
    POM_VERSION = readMavenPom file: 'pom.xml'.getVersion() 
  }
  stages {
      stage ('Build'){
        steps {
          script {
            echo "${POM_VERSION}"
          }
        }
      }
  }
}
