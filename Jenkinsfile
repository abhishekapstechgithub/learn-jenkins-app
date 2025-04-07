pipeline {
    agent any  // Run the pipeline on any available node

    environment {
        NPM_CONFIG_CACHE = "${env.WORKSPACE}/.npm-cache"

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'  // Use the Node.js Docker image
                    reuseNode true  // Reuse the workspace between stages
                }
            }
            script {
                    sh '''
                        rm -rf node_modules package-lock.json .npm-cache
                        npm ci --cache .npm-cache --prefer-offline
                    '''
                }
            }
        }
    }
}
