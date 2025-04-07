pipeline {
    agent any

    stages {
        stage('Build') {
            agent{
                docker{
                    image 'node:18-alpine'
                    reuseNode true
                }
            }
            steps {
                sh '''
                ls -la
                rm -rf node_modules
                rm package-lock.json
                npm install
                node --version
                npm --version
                npm ci
                npm run build
                ls -la

                '''
            }
        }
    }
}

