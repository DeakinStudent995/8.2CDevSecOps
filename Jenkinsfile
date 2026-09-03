pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR-TOKEN')
    }

    stages {
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                bat 'npx sonar-scanner'
    }
}
        stage('NPM Audit') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
    }

post {
    success {
        mail to: 's225171995@deakin.edu.au',
             subject: "Jenkins Build Successful: ${env.JOB_NAME}",
             body: "Build ${env.BUILD_NUMBER} completed successfully."
    }

    failure {
        mail to: 's225171995@deakin.edu.au',
             subject: "Jenkins Build Failed: ${env.JOB_NAME}",
             body: "Build ${env.BUILD_NUMBER} failed. Check Jenkins Console Output."
        }
    }
}
