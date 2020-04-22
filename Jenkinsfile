pipeline{
  agent any 
  stages {
    stage ('artifact_create') {
      steps {
          script {
              def git_commit_previos 
              def git_commit_new = "${GIT_COMMIT}"
            //adding new commit 
          }
        sh 'mvn clean install'
        archive '**/*.war'
        echo "current commit id is : ${GIT_COMMIT}"
        echo "Previous commit is : ${GIT_PREVIOUS_COMMIT}"

    
      }
    }
  }
}
