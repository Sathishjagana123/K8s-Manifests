node {
  def app

  stage('Clone repository') {
    checkout scm
  }

  stage('Update Git') {
    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
      withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
        script {
          sh 'git config user.email "satishjagana123@gmail.com"'
          sh 'git config user.name "sathishjagana123"'

          sh 'cat deployment.yaml'
          sh 'sed -i "s+dockersampath/packages.*+dockersampath/packages:${DOCKERTAG}+g" deployment.yaml'
          sh 'cat deployment.yaml'

          sh 'git add .'
          sh "git commit -m 'By Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
          sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/K8s-Manifests.git HEAD:main"
        }
      }
    }
  }
}
