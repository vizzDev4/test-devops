pipeline {
    agent any
    stages {
        #+------------------------------------------------------------------+
        #| Building Stage				                                    |
        #+------------------------------------------------------------------+
        stage('build') {
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
                        mkdir dist -p
                        touch dist/index.html
                        ls -la
                    '''
            }
        }
        #+------------------------------------------------------------------+
        #| Testing Stage				                                     |
        #+------------------------------------------------------------------+
        stage('test') {
            steps {
                    sh '''
                        test -f dist/index.html
                    '''
            }
        }
        #+------------------------------------------------------------------+
        #| PushToAWS Stage				                                     |
        #+------------------------------------------------------------------+
    }
}