pipeline {
    agent {
                docker {
                    image 'circleci/python:3.7'
                    args '-u root:root'
                }
            }

    stages {
        stage('Install Dependencies') { 
            steps {
                sh 'python3 -m venv venv' 
                sh '. venv/bin/activate'
                sh 'pip install -r requirements.txt' 
            }
        }
        stage('Run Tests') {
            steps {
                sh 'flake8 --exclude=venv* --statistics'                       
                sh 'pytest -v --cov=calculator'
            }
        }

    }
}