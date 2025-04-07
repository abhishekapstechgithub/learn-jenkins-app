pipeline {
    agent any

    environment {
        // Define Node.js version to use
        NODE_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
    }

    stages {
        stage('Preparation') {
            steps {
                // Clean up previous node_modules and install dependencies fresh
                script {
                    sh 'rm -rf node_modules'  // Clean up old node_modules
                    sh 'rm -f package-lock.json'  // Clean up package-lock to avoid potential cache issues
                }
            }
        }
        
        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure npm version is correct
                    sh 'npm --version'

                    // Install dependencies using npm ci
                    sh 'npm ci'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Running build command or any other command as per your project setup
                    sh 'npm run build'  // Or any other build command you may use
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Running tests if you have any
                    sh 'npm test'
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Cleanup after the build (Optional)
                    sh 'rm -rf node_modules'  // Remove node_modules if necessary
                    sh 'rm -f package-lock.json'  // Optional cleanup of the lock file
                }
            }
        }
    }

    post {
        always {
            // Clean up the workspace if needed
            cleanWs()
        }
    }
}
