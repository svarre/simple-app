#!/usr/bin/env groovy
pipeline {
  agent any
  parameters {
    choice(name: 'build',
          choices: 'no\nyes',
          description: 'Select yes tfor only building the war file'
    )
    choice(name: 'list',
          choices: 'no\nyes',
          description: 'Select yes for Listing the files onle'
    )
  }
  
  stages {
    stage ('Build'){
      when {
        expression {params.build == 'yes'}
      }
      steps{
        script {
          def mavenPom = readMavenPom file: 'pom.xml'
          echo "${mavenPom.version}"
          sh 'mvn clean install package'
          archiveArtifacts '**/*.war'
          stash includes: '**/*.war', name: 'build_artifacts'
          
        //  def pom = readMavenPom file:'pom.xml'
          //def pomversion = pom.version
        }
      
      }
      
    }
    stage ('ls the files'){
      when {
        expression {params.list == 'yes'}
      }
      steps{
        sh 'ls'
      }
    }
  }
}
