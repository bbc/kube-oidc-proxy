pipeline {
  agent {
    label 'docker'
  }
  stage('Package helm chart') {
    steps {
      withCredentials(
          [usernamePassword(
              credentialsId: 'e5c02db5-b9f5-4070-9750-025d8d087480',
              passwordVariable: 'HELM_PASSWORD',
              usernameVariable: 'HELM_USERNAME'
          )]
      )
      {   sh('set +e')
          sh("helm package deploy/charts/kube-oidc-proxy")
          sh("curl -u ${HELM_USERNAME}:${HELM_PASSWORD} http://nexus.jupiter.bbc.co.uk:8081/nexus/repository/helm-bsd/ --upload-file kube-oidc-proxy*.tgz -v")
          sh('rm *.tgz')
          sh('set -e')
      }
    }
  } 
}
