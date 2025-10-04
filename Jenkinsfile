pipeline {
    agent any

    environment {
        DEPLOY_PATH = "/var/www/react-app"
    }

    tools {
        nodejs "Node"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ShivaKodes/Test-project.git'
            }
        }

        stage('Install & Build') {
            steps {
                sh '''
                  npm ci --no-audit --ignore-scripts
                  npm run build
                '''
                stash includes: 'dist/**', name: 'build-artifacts'
            }
        }

        stage('Deploy') {
            steps {
                unstash 'build-artifacts'
                sh '''
                  # create deploy folder if it doesn't exist
                  rm -rf ${DEPLOY_PATH}/*
                  cp -r dist/* ${DEPLOY_PATH}/
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
