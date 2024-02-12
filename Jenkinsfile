pipeline {
    agent any

    environment {
        branchName = "${env.GIT_BRANCH.split('/').size() == 1 ? env.GIT_BRANCH.split('/')[-1] : env.GIT_BRANCH.split('/')[1..-1].join('/')}"
    }
    stages {
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
                ///sh """
                /// scp -i
                /// """
                sh ' echo "code pushed to the test branch" '
                sh 'pwd'
                sh 'ls -al'
            }
        }

        stage('Copy files to prod server') {
            agent {
                label 'test'
            }
            when {
                expression {
                    branchName == 'prod'
                }
            }
            steps {
                ///sh """
                ///scp -i
                /// """
                sh ' echo "code pushed to the prod branch" '
            }
        }
    }
}
