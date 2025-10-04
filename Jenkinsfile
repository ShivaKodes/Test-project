pipeline {
    agent any
    tools {nodejs "Node"}
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
                  rm -rf ${DEPLOY_PATH}/*
                  cp -r build/* ${DEPLOY_PATH}/
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
