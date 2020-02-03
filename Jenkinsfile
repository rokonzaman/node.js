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
    stage ("Build Code")
    {
      steps {
        sh "cd /root/rokon/nodejs/frontend/node.js && npm run build"
      }
    }
    stage ("Image Create")
    {
      steps {
        sh "docker build -t rokonzaman/nodeapp:latest /root/rokon/nodejs/frontend/node.js/."
      }
    }
    stage ("Push Image")
    {
      steps {
        sh "docker push rokonzaman/nodeapp:latest"
      }
    }
    stage ("Remove Image")
    {
      steps {
        sh "docker rmi rokonzaman/nodeapp:latest -f"
      }
    }
    stage ("Deploy")
    {
      agent {
        label "kubernetes"
      }
      steps {
        sh 'kubectl apply -f /root/nodeapp.yaml'
      }
    }
  }
}