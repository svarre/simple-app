pipeline{
  agent any

 environment {
     GIT_CURRENT_COMMIT =  "${GIT_COMMIT}"
     GIT_PREVIOUS_COMMIT = "${GIT_PREVIOUS_COMMIT}"
 }
 parameters {
     choice(name: 'build',
        choices: 'no\nyes',
        description: 'perform build')
     choice(name: 'deploy',
        choices: 'no\nyes',
        description: 'Only to deploy')
 }

  stages {
    stage ('Build') {
      when {
          expression { params.build == 'yes'}
      }
      steps {

        //sh 'mvn clean install'
        //archive '**/*.war'
        echo "current commit id is : ${GIT_COMMIT}"
        echo "Previous commit is : ${GIT_PREVIOUS_COMMIT}"    
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
    stage ('Deploy'){
        when {
            expression { params.deploy == 'yes'}
        }
        steps {
                sh 'cd artifacts'
                sh 'curl http://stash.compciv.org/ssa_baby_names/names.zip --output babynames.zip'
                sh 'ls'
            
            
            
        }
    }
  }
}
