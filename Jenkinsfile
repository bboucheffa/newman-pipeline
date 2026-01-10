pipeline {
    agent any

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
                newman run CollectionRunner.postman_collection.json
                '''
            }
        }

        stage('Rapport generate') {
            steps {

            }
        }
    }
}
