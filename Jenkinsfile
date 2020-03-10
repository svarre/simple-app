pipeline {
    agent any
    options {
        buildDiscarder logRotator(numToKeepStr: '10')
    }
    parameters{
        booleanParam(name: skipScans , defaultValue: true , description: 'Enabling this will skip!' )
        choice(name: 'ScanOnly', 
            choices: ['One', 'Two', 'Three'], 
            description: 'Select if you want to do only scan ')
    }

    stages {
        stage('Build'){
            steps{
                script {
                    currentBuild.displayName = "Test-Build - " + currentBuild.number
                }
                sh script: 'mvn clean install'
                archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
                echo "Printing parameters name ${params.ScanOnly}"
            }
        }
    }
}
