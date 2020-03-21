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
                script{
                    def mavenPom = readMavenPom file:'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"
                    nexusArtifactUploader artifacts: [
                        [
                        artifactId: 'simple-app', 
                        classifier: '', 
                        file: "target/simple-app-${mavenPom.version}.war", 
                        type: 'war'
                         ]
                    ],
                    credentialsId: 'nexus_credentials', 
                    groupId: 'in.javahome',
                    nexusUrl: '172.31.40.137:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${nexusRepoName}", 
                    version: "${mavenPom.version}"
                }
                
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
        stage('Email Notificaiton'){
            steps{
                mail bcc: '', body: '''Hi, This is a test mail ''',  
                subject: 'Build Status for Parallel Project ', to: 'sivva26@gmail.com'
            }
        }
        
    }
}
