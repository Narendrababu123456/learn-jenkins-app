pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
        
            steps {
                echo 'Hello World'
                sh '''
                    ls -la
                    npm --version
                    node --version
                    npm ci
                    npm run build
                    ls -al
                '''
            }
        }
        stage('test') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
        
            steps {
                echo 'test'
                sh '''
                    test -f build/index.html
                    npm test
                '''
            }
        }
    
        stage('e2e') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }
        
            steps {
                echo 'e2e'
                sh '''
                    npm install serve 
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                '''
            }
        }
    }    
    post {
        always {
            junit 'test-results/junit.xml'
        }
    }
}