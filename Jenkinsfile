pipeline {
    agent any

    environment {
        PORT = '3000'
    }

    stages {

        stage('Setup Node') {
            steps {
                sh '''
                    export NVM_DIR="$HOME/.nvm"
                    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"

                    nvm install $NODE_VERSION
                    nvm use $NODE_VERSION

                    node -v
                    npm -v
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
                    echo "Stopping old app..."
                    pkill -f "serve -s build" || true

                    echo "Installing serve..."
                    npm install -g serve

                    echo "Starting app..."
                    nohup serve -s build -l $PORT > app.log 2>&1 &
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