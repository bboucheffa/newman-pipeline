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
                where node || (
                    echo Node.js non installé
                    exit /b 1
                )

                where npm || (
                    echo npm non installé
                    exit /b 1
                )

                where newman || (
                    echo Installation de Newman...
                    npm install -g newman
                )
                '''
            }
        }

        stage('Run Newman') {
            steps {
                bat '''
                newman run %COLLECTION%
                '''
            }
        }

        stage('Rapport generate') {
            steps {
                bat '''
                if not exist %REPORT_DIR% mkdir %REPORT_DIR%

                newman run %COLLECTION% ^
                  -r html ^
                  --reporter-html-export %REPORT_DIR%\\report.html
                '''

            }
        }
    }
}
