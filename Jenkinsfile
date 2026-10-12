cat > Jenkinsfile <<'EOF'
pipeline {
  agent any
  triggers { pollSCM('H/2 * * * *') }
  stages {
    stage('Update site content') {
      steps {
        sh 'kubectl create configmap site-content --from-file=index.html --dry-run=client -o yaml | kubectl apply -f -'
      }
    }
    stage('Deploy') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl rollout restart deployment/myapp'
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
EOF
