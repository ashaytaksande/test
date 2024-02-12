pipeline {
    agent any

    environment {
        // Define environment variables (optional)
        // TEST_SERVER_HOST = 'your_test_server_host'
        // PROD_SERVER_HOST = 'your_prod_server_host'
        branchName = "${env.GIT_BRANCH.split('/').size() == 1 ? env.GIT_BRANCH.split('/')[-1] : env.GIT_BRANCH.split('/')[1..-1].join('/')}"
    }

    // Remove the pollSCM trigger
    // triggers {
    //     pollSCM '* * * *'
    // }

    stages {

        stage('echo variables') {
            steps {
              
                sh "echo ${branchName}"
                sh "echo ${env.BRANCH_NAME}"
            }
        }
        stage('Copy files to test server') {
            //agent {
            //      label 'test'
            //   }
            when {
                expression {
                    branchName == '(test)'
                }
            }
            steps {
                // Get the latest code from the repository
                //git branch: env.BRANCH_NAME , url: 'https://github.com/ashaytaksande/test.git'

                // Use SCP for secure file transfer
                // sh """
                // scp -i ~/.ssh/id_rsa -o StrictHostKeyChecking=no <src_directory> ${env.TEST_SERVER_HOST}:<destination_directory>
                // """
                sh ' echo "code pushed to the test branch" '
            }
        }

        stage('Copy files to prod server') {
            // agent {
            //      label 'prod'
            //  }
            when {
                expression {
                    return env.BRANCH_NAME == '(origin/prod)'
                }
            }
            steps {
                // Get the latest code from the repository
                git branch: env.BRANCH_NAME , url: 'https://github.com/ashaytaksande/test.git'

                // Use SCP for secure file transfer
                // sh """
                // scp -i ~/.ssh/id_rsa -o StrictHostKeyChecking=no <src_directory> ${env.PROD_SERVER_HOST}:<destination_directory>
                // """
                sh ' echo "code pushed to the prod branch" '
            }
        }
    }
}
