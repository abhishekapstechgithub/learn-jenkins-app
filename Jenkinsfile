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
                    sh 'node --version'
                    sh 'npm --version'
                    sh 'which npm'
                    sh 'rm -rf node_modules'
                    

                    // Clean install dependencies and build the app
                    sh 'ls -la'
                    sh 'npm install'
                    sh 'npm ci'
                    sh 'npm run build'
                    
                    // Final directory listing to ensure files exist
                    sh 'ls -la'
                }
            }
        }
    }
}
