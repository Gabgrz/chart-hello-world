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
                stage('Setup') {
                        echo "Setup step";
                        script {
                            def dockerSandbox = docker.image('dtzar/helm-kubectl:3.7.2')
                            dockerSandbox.pull()
                            dockerSandbox.inside () {
                                sh "id"
                                sh "pwd"
                                sh "ls -l"
                                sh "helm version"
                            }
                        }
                    }
                }
}
