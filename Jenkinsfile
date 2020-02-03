pipeline {
    agent none
    stages {
        stage('Checkout') {
            agent {
                label "kubernetes"
            }
            steps {
                sh 'kubectl apply -f /root/nodeapp.yaml'
            }
        }
        
    }
}