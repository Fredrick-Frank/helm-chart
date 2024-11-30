pipeline {
    agent any 

    stages {
        stage('Initialize Helm') {
            steps {
                echo 'Initializing Helm...'
                sh 'helm version'
                sh 'helm ls'
            }
        }

        stage('Lint Helm Chart') {
            steps {
                echo 'Linting Helm Chart...'
                sh 'helm lint ./helm'
            }
        }

        stage('Deploy Application') {
            steps {
                echo 'Deploying Application with Helm...'
                sh '''
                helm upgrade --install test-helm ./helm
                '''
            }
        }

        stage('Verify Deployment and Helm List') {
            steps {
                echo 'Verifying Deployment...'
                sh 'helm ls'
                sh 'kubectl get pods'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful'
        }
        failure {
            echo 'Pipeline Failed. Troubleshoot the error!'
        }
    }
}

