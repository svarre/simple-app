#!/usr/bin/env groovy
pipeline{
  agent any
  environment {
    POM_VERSION = readMavenPom file: 'pom.xml'.version 
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
