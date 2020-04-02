pipeline{
    agent any 
    stages{
        stage('Build the war file'){
            steps{
                sh script: 'mvn clean package'
                sh 'ls'
            }
            post {
                success {
                    stash includes: 'target/*.war', name: 'build_artifact'
                }
            }
        }
    }
}
