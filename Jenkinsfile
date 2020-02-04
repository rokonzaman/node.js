pipeline {
    agent none
    stages {
        stage('Checkout') {
            agent {
                label "nodejs"
            }
            steps {
                git 'https://github.com/rokonzaman/node.js.git'
            }
        }
        stage('Build Code') {
            agent {
                label "nodejs"
            }
            steps {
                sh "cd /root/rokon/jenkins_agent/node.js/workspace/Node.js_master && npm run build"
            }
        }
        stage('Image Create') {
            agent {
                label "nodejs"
            }
            steps {
                sh "docker build -t rokonzaman/nodeapp:latest /root/rokon/jenkins_agent/node.js/workspace/Node.js_master/."
            }
        }
        stage('Push Image') {
            agent {
                label "nodejs"
            }
            steps {
                sh "docker push rokonzaman/nodeapp:latest"
            }
        }
        stage('Remove Image') {
            agent {
                label "nodejs"
            }
            steps {
                sh "docker rmi rokonzaman/nodeapp:latest -f"
            }
        }
        stage('Deploy') {
            agent {
                label "kubernetes"
            }
            steps {
                sh 'kubectl apply -f /root/nodeapp.yaml'
            }
        }
        stage('Rollout') {
            agent {
                label "kubernetes"
            }
            steps {
                sh 'kubectl rollout restart deployment.apps/nodeapp-deploy'
            }
        }
        
    }
}