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
                sh "cd /root/rokon/jenkins_agent/workspace/Node.js_master && npm run build"
            }
        }
        stage('Image Create') {
            agent {
                label "nodejs"
            }
            steps {
                sh "docker build -t rokonzaman/nodeapp:1.0 /root/rokon/jenkins_agent/workspace/Node.js_master/."
            }
        }
        stage('Push Image') {
            agent {
                label "nodejs"
            }
            steps {
                sh "docker push rokonzaman/nodeapp:1.0"
            }
        }
        stage('Remove Image') {
            agent {
                label "nodejs"
            }
            steps {
                sh "docker rmi rokonzaman/nodeapp:1.0 -f"
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