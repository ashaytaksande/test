pipeline {
    agent any

    environment {
        branchName = "${env.GIT_BRANCH.split('/').size() == 1 ? env.GIT_BRANCH.split('/')[-1] : env.GIT_BRANCH.split('/')[1..-1].join('/')}"
    }
    stages {
        stage('echo variables') {
            steps {
                sh "echo ${branchName}"
            }
        }
        stage('Copy files to test server') {
            agent {
                label 'test'
               }
            when {
                expression {
                    branchName == 'test'
                }
            }
            steps {
                // Get the latest code from the repository
                git branch:'test', url: 'https://github.com/ashaytaksande/test.git'

                // Use SCP for secure file transfer
                // sh """
                // scp -i ~/.ssh/id_rsa -o StrictHostKeyChecking=no <src_directory> ${env.TEST_SERVER_HOST}:<destination_directory>
                // """
                sh ' echo "code pushed to the test branch" '
                sh 'pwd'
                sh 'ls -al'
            }
        }

        stage('Copy files to prod server') {
            // agent {
            //      label 'prod'
            //  }
            when {
                expression {
                    branchName == 'prod'
                }
            }
            steps {
                // Get the latest code from the repository
                git branch:'prod', url: 'https://github.com/ashaytaksande/test.git'

                // Use SCP for secure file transfer
                // sh """
                // scp -i ~/.ssh/id_rsa -o StrictHostKeyChecking=no <src_directory> ${env.PROD_SERVER_HOST}:<destination_directory>
                // """
                sh ' echo "code pushed to the prod branch" '
            }
        }
    }
}