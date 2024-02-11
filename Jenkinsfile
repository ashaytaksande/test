pipeline {
    agent any
    stages {
        stage('Copy files to test server') {
            steps {
                // Get the latest code from the repository
                git branch: 'test' , url: 'https://github.com/ashaytaksande/test.git'

                // Use SCP for secure file transfer
               // sh """
               // scp -i ~/.ssh/id_rsa -o StrictHostKeyChecking=no <src_directory> ${env.TEST_SERVER_HOST}:<destination_directory>
               // """
                  sh ' echo "code pushed to the test branch" '
                  sh 'git branch'
                  sh 'git branch -r'
            }
        }

    }
}

