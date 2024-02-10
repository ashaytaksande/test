pipeline {
    agent any
    environment {
        sshkey=credentials('key')
    }

    stages {
        stage('checkout') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/ashaytaksande/test.git'
                sh 'whoami'
            }
        }
        stage('copy git files to test server') {
            steps {
                sh 'ls -al'
                sh 'scp -i ${sshkey} -p -r $(pwd) ubuntu@ec2-44-201-117-222.compute-1.amazonaws.com:/home/ubuntu/ass'
            }
        }
            
        }
    }

