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
          script {
                string a = "${GIT_CURRENT_COMMIT}"
                println("Substring of present commit is : ${a}.substring(0,6)")
                sh 'mvn clean install'
                archive '**/*.war'
                echo "current commit id is : ${GIT_COMMIT}"
                echo "Previous commit is : ${GIT_PREVIOUS_COMMIT}"
                }


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
    stage ('Deploy to stage') {
       when { 
         branch pattern: "release/\\d{1,2}\\-d{1,2}\\-\\d{1.2}", comparator: "REGEXP"
         expression { params.deploy == 'yes' }
       }
       steps {
         echo "Executing branch in stage"
       }
       
    }

  }
}
