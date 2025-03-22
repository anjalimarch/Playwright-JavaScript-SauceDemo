pipeline {
    agent any
    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/anjalimarch/Playwright-JavaScript-SauceDemo.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
                bat 'npx playwright install'
            }
        }
        stage('Run Playwright Tests') {
            steps {
                bat 'npx playwright test'
            }
        }
    }
   post {
    always {
        script {
            node {
                archiveArtifacts artifacts: '**/test-results/**', fingerprint: true
            }
        }
    }
}
}
