pipeline {
    agent any
    environment { 
        folder_name = "build_folder"
    }
    stages {
        stage('build:dev') {
            steps {
                script { 
                    sh 'pwd'
                    cleanWs()
                    echo 'Creating Directory dist'
                    sh "mkdir -p ${folder_name}" 
                    echo 'Creating file inside dist'
                    sh "touch ${folder_name}/index.txt" 
                    echo 'Building Project Done'
                }
            }
        }
    }
}
