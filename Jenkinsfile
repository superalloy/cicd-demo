pipeline {
    agent none

    stages {
        // stage('Checkout') {
        //     steps {
        //         git url: 'https://github.com/superalloy/cicd-demo.git', branch: 'main'
        //     }
        // }

        stage('Setup env') {
            agent any 
            steps {
                script {
                    sh '''
                        python -m venv .venv
                        source .venv/bin/activate
                        pip install -r requirements.txt
                        pip install -r test-requirements.txt
                    '''
                }
            }
        }

        stage('lint') {
            agent any
            steps {
                script {
                    sh '''
                        source .venv/bin/activate
                        pip install flake8
                        flake8 .
                    '''
                }
            }
        }
        stage('test') {
            agent any
            steps {
                script {
                    sh '''
                        source .venv/bin/activate
                        pytest --verbose --junit-xml results.xml
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
