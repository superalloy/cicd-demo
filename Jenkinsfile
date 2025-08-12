pipeline {
    agent none

    stages {
        // stage('Checkout') {
        //     steps {
        //         git url: 'https://github.com/superalloy/cicd-demo.git', branch: 'main'
        //     }
        // }

        stage('Setup env') {
            agent {
                docker {
                    image 'python:3.11-alpine'
                }
            }
            steps {
                script {
                    sh '''
                        pip install -r requirements.txt
                        pip install -r test-requirements.txt
                    '''
                }
            }
        }

        stage('lint') {
            agent {
                docker {
                    image 'python:3.11-alpine'
                }
            }
            steps {
                script {
                    sh '''
                        pip install flake8
                        flake8 .
                    '''
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
