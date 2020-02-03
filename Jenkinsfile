pipeline {
  agent none
  stages {
    stage ("Checkout")
      agent { label "nodejs" }
    {
      steps {
        git 'https://github.com/rokonzaman/node.js.git'
      }
    }
    stage ("Build Code")
      agent { label "nodejs" }
    {
      steps {
        sh "cd /root/rokon/nodejs/frontend/node.js && npm run build"
      }
    }
    stage ("Image Create")
      agent { label "nodejs" }
    {
      steps {
        sh "docker build -t rokonzaman/nodeapp:latest /root/rokon/nodejs/frontend/node.js/."
      }
    }
    stage ("Push Image")
      agent { label "nodejs" }
    {
      steps {
        sh "docker push rokonzaman/nodeapp:latest"
      }
    }
    stage ("Remove Image")
      agent { label "nodejs" }
    {
      steps {
        sh "docker rmi rokonzaman/nodeapp:latest -f"
      }
    }
    stage ("Deploy")
      agent { label "kubernetes" }
    {
      steps {
        sh 'kubectl apply -f /root/nodeapp.yaml'
      }
    }
  }
}