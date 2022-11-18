pipeline {
  agent any
  stages {
    stage ('Clone repo'){
      steps {
        checkout scm
      }
     stage('Update Manifest') {
       steps{
      script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                  //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                  sh "git config user.email bhairavi.sanskriti@gmail.com"
                  sh "git config user.name BhairaviSanskriti"
                  //sh "git switch master"
                  sh "cat deployment.yaml"
                  sh "sed -i 's+bhairavisanskriti/sanskriti-portfolio.*+bhairavisanskriti/sanskriti-portfolio:${BUILDNUMBER}+g' deployment.yaml"
                  sh "cat deployment.yaml"
                  sh "git add ."
                  sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                  sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Jenkins-Update-Manifest.git HEAD:main"
              }
           }
        }
      }
     }
    }
    }
}
