pipeline {
    agent any
     environment {
        EC2_USER = 'ec2-user' 
        EC2_HOST = 'ec2-18-246-219-6.us-west-2.compute.amazonaws.com'
    }
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
                sshagent(['18.246.219.6']) { 
                    sh '''
                    echo Connection successful!
                    ls -la 
                    '''
                    sh "ssh -o StrictHostKeyChecking=no ${EC2_USER}@${EC2_HOST} 'touch testk.html'"
                }
            }
        }
    }
}


// we can run these in parrallel too ... by adding parallel { stages }