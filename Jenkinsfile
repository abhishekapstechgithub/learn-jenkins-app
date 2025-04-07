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
           

                    // Clean install dependencies and build the app
                    sh 'sudo npm ci'
                    sh 'sudo npm run build'
                    
                    // Final directory listing to ensure files exist
                    sh 'ls -la'
                }
            }
        }
    }
}
