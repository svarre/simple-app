pipeline{
    agent any 
    stages{
        stage('Build the war file'){
            steps{
                sh script: 'mvn clean package'
                sh 'ls'
                sh 'ls target/'
            }
            post {
                success {
                    stash includes: 'target/*.war', name: 'build_artifact'
                }
            }
        }
    }
}
