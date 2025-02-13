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
                    ls -al
                    npm run build
                '''    
            }
        }        
    }
}