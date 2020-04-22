pipeline{
  agent any 
  stages {
    stage ('artifact_create') {
      steps {
          script {
              def GIT_CURRENT_COMMIT =  "${GIT_COMMIT}"
              def GIT_PREVIOUS_COMMIT = "${GIT_PREVIOUS_COMMIT}"
              
          }
        sh 'mvn clean install'
        archive '**/*.war'
        echo "current commit id is : ${GIT_COMMIT}"
        echo "Previous commit is : ${GIT_PREVIOUS_COMMIT}"
    
      }
      post {
          success {
              script {
                  if (GIT_CURRENT_COMMIT == GIT_PREVIOUS_COMMIT) {
                      echo "skipping uploading to artifact"
                  }

                  else {
                      echo "Uploading to artifacts "
                  }
              }
          }
      }
    }
  }
}
