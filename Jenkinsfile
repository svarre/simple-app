pipeline{
  agent any

 environment {
     GIT_CURRENT_COMMIT =  "${GIT_COMMIT}"
     GIT_PREVIOUS_COMMIT = "${GIT_PREVIOUS_COMMIT}"
 }

  stages {
    stage ('artifact_create') {
      steps {

        sh 'mvn clean install'
        archive '**/*.war'
        echo "current commit id is : ${GIT_COMMIT}"
        echo "Previous commit is : ${GIT_PREVIOUS_COMMIT}"
        sh 'curl http://stash.compciv.org/ssa_baby_names/names.zip --output babynames.zip'
        sh 'ls'
    
      }
      post {
          success {
              script {
                  if (env.GIT_CURRENT_COMMIT == env.GIT_PREVIOUS_COMMIT) {
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
