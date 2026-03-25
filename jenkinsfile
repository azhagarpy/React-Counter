pipeline {
    agent any

    environment {
        NODE_VERSION = '23'
        APP_NAME = 'react-app'
        PORT = '3000'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/your-username/your-repo.git'
            }
        }

        stage('Setup Node') {
            steps {
                sh '''
                    nvm use $NODE_VERSION
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Run App') {
            steps {
                sh '''
                    echo "Stopping old app if running..."
                    pkill -f "serve -s build" || true

                    echo "Installing serve package..."
                    pm start

                    echo "App started..."
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}