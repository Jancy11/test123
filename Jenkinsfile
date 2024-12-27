pipeline {
    agent any
    environment {
        PYTHON_PATH = 'C:\\Users\\Admin\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\Admin\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat """
                set PATH=%PYTHON_PATH%;%PATH%
                pip install -r requirements.txt
                """
            }
        }
        stage('Sonarqube-Analysis') {
            environment {
                SONAR_TOKEN = credentials('sonar-token')
            }
            steps {
                bat """
                set PATH=%PYTHON_PATH%;%PATH%
                sonar-scanner -Dsonar.projectKey=test110 ^
                               -Dsonar.sources=. ^
                               -Dsonar.host.url=http://localhost:9000 ^
                               -Dsonar.login=%SONAR_TOKEN%
                """
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
        always {
            echo 'This runs regardless of the result.'
        }
    }
}
