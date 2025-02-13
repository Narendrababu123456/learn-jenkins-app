pipeline {
    agent any

    stages {
        stage('without Docker') {
            steps {
                sh 'echo "without Docker"'
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
                sh 'echo "with Docker"'
                sh 'npm --version'
            }
        }        
    }
}