pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t myapp:${BUILD_NUMBER} .'
      }
    }
    stage('Deploy') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
      }
    }
    stage('Verify') {
      steps {
        sh 'kubectl rollout status deployment/myapp --timeout=120s'
        sh 'kubectl get pods'
      }
    }
  }
}
