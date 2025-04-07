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
                    sh '/usr/local/bin/npm cache clean -force'
           

                    // Clean install dependencies and build the app
                    sh '/usr/local/bin/npm install'
                    sh '/usr/local/bin/npm ci'
                    sh '/usr/local/bin/npm run build'
                    
                    // Final directory listing to ensure files exist
                    sh 'ls -la'
                }
            }
        }
    }
}
