node {
    def app
    stage('Clone repository') {
        checkout scm
    }
 stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'GitHub', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email hilerytaylorjr@gmail.com"
                        sh "git config user.name htaylor"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+ltartsmusic/gitopswebproject.*+ltartsmusic/gitopswebproject:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/gitops_manifest_local.git HEAD:main"
         }
       }
     }
   }
 }
