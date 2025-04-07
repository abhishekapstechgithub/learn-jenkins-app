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
                cleanWS()
                sh '''
                ls -la
                sudo apt install git -y
                sudo chown -R 114:121 "/.npm"
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

