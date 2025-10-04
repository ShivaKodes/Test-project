pipeline {
    agent any

    environment {
        DEPLOY_PATH = "/var/www/html"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ShivaKodes/Test-project.git'
            }
        }

        stage('Build') {
            agent {
                docker { image 'node:18' }   // run build in Node.js container
            }
            steps {
                sh '''
                  npm ci --no-audit --ignore-scripts
                  npm run build
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  sudo rm -rf ${DEPLOY_PATH}/*
                  sudo cp -r build/* ${DEPLOY_PATH}/
                '''
            }
        }
    }

    post {
        always {
            echo "Pipeline completed!"
        }
    }
}
