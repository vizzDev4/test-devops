pipeline {
    agent any
    
    stages {
      
        //+------------------------------------------------------------------+
        //| Building Stage				                                    |
        //+------------------------------------------------------------------+
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
        //+------------------------------------------------------------------+
        //| Testing Stage				                                     |
        //+------------------------------------------------------------------+
        stage('test') {
            steps {
                    sh '''
                        ls -la
                        test -f dist/index.html
                    '''
            }
        }
        //+------------------------------------------------------------------+
        //| PushToAWS Stage				                                     |
        //+------------------------------------------------------------------+
        stage('EC2:Push') {
            steps {
                sshagent(['ec2-user (ec2user)']) { 
                    // Copy folder to the EC2 instance
                    sh '''
                    echo "Connection successful!"
                    '''
                }
            }
        }
    }
}


// we can run these in parrallel too ... by adding parallel { stages }