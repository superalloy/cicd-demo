pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/superalloy/cicd-demo.git', branch: 'main'
            }
        }

        stage('Setup env') {
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
            steps {
                script {
                    sh '''
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
