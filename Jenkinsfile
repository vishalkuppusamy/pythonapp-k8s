node {
  stage('Clone Repo') {
    checkout scm
  }
  stage('Update Manifest File') {
    script {
      catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(
                    credentialsId: 'github',
                    usernameVariable: 'GIT_USERNAME',
                    passwordVariable: 'GIT_PASSWORD'
                )]) {
                  sh """

                git config user.email "kuppusav@gmail.com"
                git config user.name "kuppusav"

                echo "K8s-app.yaml before the update"
                cat k8s-app.yaml

                sed -i 's+kuppusav/pythonapp.*+kuppusav/pythonapp:${DOCKERTAG}+g'
                cat k8s-app.yaml
                git add .
                git commit -m 'ob is update: $(env.BUILD_NUMBER)'
                git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/pythonapp-k8s.git HEAD: main

                """
                }
      }
