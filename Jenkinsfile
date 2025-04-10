pipeline {
    agent any  // Run the pipeline on any available node


    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'  // Use the Node.js Docker image
                    reuseNode true  // Reuse the workspace between stages
                }
            }
            steps {
                script {
                    // Printing out the directory contents and versions
                    sh 'ls -la'
                    
                    sh 'npm install --cache .npm-cache'
                    
                    sh 'npm install --cache .npm-cache --prefer-offline'

                    sh 'npm run build'
              
                    sh 'ls -la'
                }
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'node:18-alpine'  // Use the Node.js Docker image
                    reuseNode true  // Reuse the workspace between stages
                }
            }
            
            steps {
                echo 'Test stage....'
                sh 'test -f build/index.html'
                sh 'npm test'
            }
        }
        stage('E2E') {
            agent {
                docker {
                    image 'mcr.microsoft.com/playwright:v1.39.0-jammy'
                    reuseNode true
                }
            }

            steps {
                sh '''
                    npm install serve --cache .npm-cache --prefer-offline
                    node_modules/.bin/serve -s build &
                    sleep 10
                    npx playwright test
                '''
            }
        }    
    }
    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
}
