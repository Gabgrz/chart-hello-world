 // A pipeline for a hello world helm chart
 pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        metadata:
          labels:
            some-label: some-label-value
        spec:
          containers:
          - name: maven
            image: maven:alpine
            command:
            - cat
            tty: true
          - name: busybox
            image: busybox
            command:
            - cat
            tty: true
          - name: helm
            image: dtzar/helm-kubectl
            command:
            - cat
            tty: true            
        '''
    }
  }
  stages {
    stage('Check helm version') {
      steps {
        container('maven') {
          sh 'mvn -version'
        }
        container('busybox') {
          sh '/bin/busybox'
        }
        container('helm') {
          sh 'helm version && \
          helm repo add cloudecho https://cloudecho.github.io/charts && \
          helm install my-hello cloudecho/hello -n default --version=0.1.2'
        }        
      }
    }
  }
}
