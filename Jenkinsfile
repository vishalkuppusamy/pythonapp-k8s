node {
    def app

    stage('Clone Repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(
                    credentialsId: 'github',
                    passwordVariable: 'GIT_PASSWORD',
                    usernameVariable: 'GIT_USERNAME'
                )]) {
                    sh 'git config user.email "kuppusav@gmail.com"'
                    sh 'git config user.name "kuppusav"'

                    sh 'echo "Before update:"'
                    sh 'cat k8s-app.yaml'

                    sh 'sed -i "s+kuppusav/pythonapp:+kuppusav/pythonapp:$DOCKERTAG+g" k8s-app.yaml'

                    sh 'echo "After update:"'
                    sh 'cat k8s-app.yaml'

                    sh 'git add k8s-app.yaml'
                    sh 'git commit -m "Done by Jenkins Job changemanifest: $BUILD_NUMBER"'
                    sh 'git push https://$GIT_USERNAME:$GIT_PASSWORD@github.com/$GIT_USERNAME/pythonapp-k8s.git HEAD:main'
                }
            }
        }
    }
}
