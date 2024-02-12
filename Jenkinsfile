pipeline {
    agent any

    environment {
        branchName = "${env.GIT_BRANCH.split('/').size() == 1 ? env.GIT_BRANCH.split('/')[-1] : env.GIT_BRANCH.split('/')[1..-1].join('/')}"
        key = credentials('key')
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
                sh "echo ${pwd}"
                sh '''
                scp -i ${key} $(pwd) ubuntu@ec2-3-95-163-23.compute-1.amazonaws.com:/home/ubuntu/
                '''
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
