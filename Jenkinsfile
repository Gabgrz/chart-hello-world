podTemplate(yaml: '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: docker
    image: docker:19.03.1-dind
    securityContext:
      privileged: true
    env:
      - name: DOCKER_TLS_CERTDIR
        value: ""
''') {
    node(POD_LABEL) {
      stage('Check docker version') {
        container('docker') {
          sh 'docker version && \
          docker pull dtzar/helm-kubectl:3.7.2'
        }
      }
      stage('Check helm version') {
        container('docker') {
          sh 'helm version'
        }
      }      
    }
}
