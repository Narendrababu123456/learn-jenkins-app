pipeline {
    agent any

    stages {
        stage('without Docker') {
            steps {
                sh '''
                    echo "without Docker"
                    ls -lart
                '''
            }
        }
        stage('with Docker') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "with Docker"
                    npm --version
                    npm ci
                    npm run build
                    ls -al
                '''    
            }
        }        
    }
}