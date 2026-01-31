pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {
        stage('Setup Python Virtual Environment') {
            steps {
                sh '''
                    python3 --version
                    python3 -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    . ${VENV_DIR}/bin/activate
                    if [ -f requirements.txt ]; then
                        pip install -r requirements.txt
                    fi
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                    . ${VENV_DIR}/bin/activate
                    python -m unittest dicover -v
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Unit tests passed successfully!'
        }
        failure {
            echo '❌ Unit tests failed!'
        }
        always {
            echo '🧹 Pipeline finished'
        }
    }
}
