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
                        python3 -m venv .venv
                        source .venv/bin/activate
                        pip3 install -r requirements.txt
                        pip3 install -r test-requirements.txt
                    '''
                }
            }
        }

        stage('lint') {
            agent any
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                
                // warnError('Optional: Command failed but pipeline continues') {
                    script {
                        sh '''
                            source .venv/bin/activate
                            pip3 install flake8
                            flake8 .
                        '''
                    }
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
