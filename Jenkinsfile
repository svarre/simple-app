pipeline {
    agent any
    tools {
        maven 'maven3.6.3'
    }
    stages {
         stage('Build'){
            steps{
                script{
                    def pom = readMavenPom file:'pom.xml'
                    def version = "App" + "-" + pom.version + "-" + currentBuild.number
                    currentBuild.displayName = version
                }
                sh 'mvn clean install'
                sh 'ls'
                //echo 'Building the stage'
            }
        }
        stage('Upload war to nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: 'target/simple-app-1.0.0.war', 
                        type: 'war'
                    ]
                ],
                credentialsId: 'nexus_credentials', 
                groupId: 'in.javahome',
                nexusUrl: '172.31.40.137:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'http://52.205.222.94:8081/repository/simpleapp-release/', 
                version: '1.0.0'
            }
        }
        stage('Stages Running in Parallel / Scans') {
            failFast true
            parallel {
                stage('Sonar Scan') {
                    steps {
                        echo "Stage1 executing"
                        sleep 10
                    }
                }
                stage('Fortify Scan') {
                    steps {
                        echo "Stage2 executing"
                        sleep 10
                    }
                }
                /*stage('Stage3') {
                    steps {
                        echo "Stage3 executing"
                        sleep 10
                    }                    
                }*/
            }
        }
        stage('Build and push Docker image'){
            steps{
                echo 'Building and pushing docker image to artifactory'
            }
        }
        stage('Deploy to Dev environment '){
            steps{
                echo 'Deploying to dev environment'
            }
        }
        stage('Test'){
            steps{
                timeout(time: 10, unit: 'SECONDS') {
                    input message:"Promoto to test" , ok:"OK"
                    
                }
                
            echo 'Promote to test'
            }
        }
        
    }
}
