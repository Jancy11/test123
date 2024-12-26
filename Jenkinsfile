pipeline {
    agent any
    environment {
        PYTHON_PATH = 'C:\\Users\\Admin\\AppData\\Local\\Programs\\Python\\Python313;C:\\Users\\Admin\\AppData\\Local\\Programs\\Python\\Python313\\Scripts'
    }
    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('build') {
            steps {
                bat """
                set PATH=%PYTHON_PATH%;%PATH%
                "C:\\Windows\\System32\\cmd.exe" /c pip install -r requirements.txt
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
                "C:\\Windows\\System32\\cmd.exe" /c sonar-scanner -Dsonar.projectKey=test110 ^
                  -Dsonar.sources=. ^
                  -Dsonar.host.url=http://localhost:9000 ^
                  -Dsonar.token=%SONAR_TOKEN%
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
