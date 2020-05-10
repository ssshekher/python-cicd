pipeline {
    agent {
                docker {
                    image 'jchaudhu/pytest:t4'
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
                sh 'pytest -v --cov=calculator --junit-xml test-reports/results.xml --cov-report xml:test-reports/coverage.xml'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                    step([$class: 'CoberturaPublisher',
                                   autoUpdateHealth: false,
                                   autoUpdateStability: false,
                                   coberturaReportFile: 'test-reports/coverage.xml',
                                   failNoReports: false,
                                   failUnhealthy: false,
                                   failUnstable: false,
                                   maxNumberOfBuilds: 10,
                                   onlyStable: false,
                                   sourceEncoding: 'ASCII',
                                   zoomCoverageChart: false])
                }
            }
        }

    }
}
