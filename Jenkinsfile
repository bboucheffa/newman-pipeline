pipeline {
    agent any

    environment {
        COLLECTION = 'CollectionRunner.postman_collection.json'
        REPORT_DIR = 'newman-report'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Dependencies install') {
            steps {
                bat '''
                node --version

                npm --version

                npm install newman newman-reporter-htmlextra --no-save
                '''
            }
        }

        stage('Run Newman') {
            steps {
                bat '''
                npx newman run %COLLECTION%
                '''
            }
        }

        stage('Rapport generate') {
            steps {
                bat '''
                if not exist %REPORT_DIR% mkdir %REPORT_DIR%

                npx newman run %COLLECTION% ^
                -r htmlextra ^
                --reporter-htmlextra-export %REPORT_DIR%\\report.html
                '''
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'newman-report/report.html', allowEmptyArchive: true 
        }
    }
}
