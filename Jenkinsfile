pipeline {
    agent any
    stages {
        stage('build:dev') {
            agent {
                docker {
                    image  'node:alpine'
                    reuseNode true
                }   
            }
            steps {
                    sh '''
                        pwd
                        ls -la
                        node --version
                        npm --version
                        npm ci
                        npm run dev
                        ls -la
                    '''
            }
        }
    }
}
