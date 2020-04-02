pipeline{
    agent any 
    stages{
        stage('Build the war file'){
            steps{
                sh script: 'mvn clean package'
                sh 'ls'
                sh 'ls target/'
                sh 'mv target/*.war target/old.war'
                sh 'ls target/'
            }
            post {
                success {
                    stash includes: 'target/*.war', name: 'build_artifact'
                }
            }
        }
        stage ('Copy Stashed files'){
            steps{
                unstash 'build_artifact'
                sh 'ls'
            }
        }
    }
}
