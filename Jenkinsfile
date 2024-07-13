pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // This checks if 'npm ci' fails, if so, it runs 'npm install'
                    if (sh(returnStatus: true, script: 'npm ci') != 0) {
                        sh 'npm install'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
