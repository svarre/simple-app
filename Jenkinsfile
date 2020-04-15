#!/usr/bin/env groovy
pipeline{
  agent any
  environment {
    POM_VERSION = readMavenPom file: 'pom.xml'
    version = POM_VERSION.version
  }
  stages {
      stage ('Build'){
        steps {
          script {
            echo "${version}"
          }
        }
      }
  }
}
