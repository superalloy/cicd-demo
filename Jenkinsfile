pipeline {
    agent any

    stages {
        // stage('Checkout') {
        //     steps {
        //         git url: 'https://github.com/your-username/my-web-app.git', branch: 'main'
        //     }
        // }

        stage('Setup env') {
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
            steps {
                script {
                    sh ''' 
                        source .venv/bin/activate
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
