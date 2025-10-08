pipeline {
    agent any

    environment {
        DEPLOY_DIR = 'C:\\inetpub\\wwwroot'  // For Windows IIS
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning project from GitHub...'
                git branch: 'main', url: 'https://github.com/<youruser>/web-ci-cd-demo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building project...'
                bat 'dir'    // (Use `sh "ls"` on Linux)
            }
        }

        stage('Test') {
            steps {
                echo 'Testing HTML syntax...'
                bat 'tidy -e index.html || exit 0'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying files to IIS folder...'
                bat 'xcopy /Y *.* %DEPLOY_DIR%\\'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline finished successfully! Visit http://localhost/index.html'
        }
        failure {
            echo '❌ Pipeline failed! Check build logs.'
        }
    }
}
