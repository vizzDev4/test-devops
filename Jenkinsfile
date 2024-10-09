pipeline {
    agent any
    stages {
        stage('build:dev') {
            agent {
                docker {
                    image  'node'
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
                        ls -la
                    '''
            }
        }
    }
}
