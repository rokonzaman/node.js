pipeline {
  agent {
        label "nodejs"
  }
  stages {
    stage ("Checkout")
    {
      steps {
        git 'https://github.com/rokonzaman/node.js.git'
      }
    }
    stage ("Test Code")
    {
      steps {
        sh "cd /root/rokon/nodejs/frontend/node.js && npm run test"
      }
    }
    stage ("Build Code")
    {
      steps {
        sh "cd /root/rokon/nodejs/frontend/node.js && npm run build"
      }
    }
    stage ("Push")
    {
      steps {
        sh "docker push rokonzaman/rolling-update-app:3.0"
      }
    }
    stage ("Deployment")
    {
      steps {
        sh "kubectl -n private apply -f ~/nginx.yaml"
      }
    }
  }
}
