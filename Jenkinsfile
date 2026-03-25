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
                git branch: 'main', url: 'https://github.com/azhagarpy/React-Counter.git'
            }
        }

        stage('Setup Node') {
            steps {
                steps {
                    sh '''
                        export NVM_DIR="$HOME/.nvm"
                        [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
                        [ -s "$NVM_DIR/bash_completion" ] && . "$NVM_DIR/bash_completion"

                        nvm install $NODE_VERSION
                        nvm use $NODE_VERSION

                        node -v
                        npm -v
                        '''
                    }

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