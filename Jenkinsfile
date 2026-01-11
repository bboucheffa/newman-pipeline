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

                npm install newman --no-save
                npm install newman-reporter-html --no-save
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
                  -r html ^
                  --reporter-html-export %REPORT_DIR%\\report2.html
                '''
            }
        }
    }
}
