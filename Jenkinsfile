pipeline {
    agent none
    options {
        buildDiscarder logRotator(numToKeepStr: '10')
    }

    stages {
        stage('Build'){
            steps{
                sh script: 'mvn clean install'
                archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
    }
}