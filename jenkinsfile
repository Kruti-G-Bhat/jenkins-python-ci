pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo 'Source code checked out'
            }
        }

        stage('Setup Python') {
            steps {
                sh 'python3 --version'
                sh 'python3 -m venv .venv'
                sh '.venv/bin/python -m pip install --upgrade pip'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '.venv/bin/python -m pip install -r requirements.txt'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '.venv/bin/python -m pytest -v'
            }
        }
    }

    post {
        success {
            echo 'All unit tests passed!'
        }

        failure {
            echo 'Build or tests failed. Check Console Output.'
        }

        always {
            echo 'CI pipeline finished.'
        }
    }
}
