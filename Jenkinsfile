pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube-Server'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/vishalkuppusamy/sonarqubecheck.git', branch: 'main'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    script {
                        def scannerHome = tool 'SonarScanner'
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

        stage('Wait for Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
