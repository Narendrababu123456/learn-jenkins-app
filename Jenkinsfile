pipeline {
    agent any
    environment {
        NETILFY_SITE_ID = '2e4ab58f-715c-4d63-906b-e8b5984e05e8'
    }

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
        stage('Deploy') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
        
            steps {
                echo 'Netilfy'
                sh '''
                    npm install netlify
                    node_modules/.bin/netlify --version
                    echo "site id $NETILFY_SITE_ID"
                    node_modules/.bin/netlify status
                '''
            }
        }        
    }    
    post {
        always {
            junit 'jest-results/junit.xml'
        }
    }
}