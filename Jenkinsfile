#!/usr/bin/env groovy
pipeline {
  agent any
  stages {
    stage ('Build'){
      steps{
        script {
          def mavenPom = readMavenPom file: 'pom.xml'
          
        //  def pom = readMavenPom file:'pom.xml'
          //def pomversion = pom.version
        }
        echo "${mavenPom.version}"
        sh 'mvn clean install package'
        archiveArtifacts '**/*.war'
      }
      
    }
  }
}
