pipeline {
    agent any
    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/anjalimarch/Playwright-JavaScript-SauceDemo.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
                sh 'npx playwright install'
            }
        }
        stage('Run Playwright Tests') {
            steps {
                sh 'npx playwright test'
            }
        }
        stage('Publish Test Report') {
            steps {
                junit '**/test-results.xml' // Ensure Playwright outputs JUnit-style results
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/test-results/**', fingerprint: true
        }
    }
}
