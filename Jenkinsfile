node {
    def app

    stage('Cloning the repository') {
        checkout scm
    }

    stage('Updating repository') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email anujapathak998@gmail.com"
                    sh "git config user.name Anujakumari"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+anuja9431/helloworld.*+anuja9431/helloworld:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job change-manifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Kubernetes-Manifest.git HEAD:main"
                }
            }
        }
    }
}