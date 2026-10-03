pipeline {
    agent any

    environment {
        DOCKER = 'C:/Users/geeth/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat "\"%DOCKER%\" build --no-cache -t vite-app ."
            }
        }

        stage('Deploy Container') {
            steps {
                bat '''
                    "%DOCKER%" stop vite-container
                    if %ERRORLEVEL% NEQ 0 echo Container not running

                    "%DOCKER%" rm vite-container
                    if %ERRORLEVEL% NEQ 0 echo Container not found

                    "%DOCKER%" run -d -p 8081:80 --name vite-container vite-app
                '''
            }
        }
    }
}
