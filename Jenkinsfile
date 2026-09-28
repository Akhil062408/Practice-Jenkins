pipeline{
    agent any

    parameters{
        string(
            name:'APP_PORT',
            defaultVALUE:'3000',
            description:'Server Port'
        )
    }

    environment{
        IMAGE_NAME='jenkins-demo-app'
    }

    stages{
        stage('Checkout'){
            steps{
                echo 'Checking out source code from Git Repo'
                Checkout scm
            }
        }
        stage('Check Docker'){
            steps{
                bat 'docker --version'
            }
        }
        stage('Dependencies'){
            steps{
                bat 'npm install'
            }
        }
        stage('Test APP'){
            steps{

            }
        }
        stage('Build'){
            steps{
                bat 'docker build -t %IMAGE_NAME%:%BUILD_NUMBER% .'
            }
        }
        stage{
            steps{
                bat '''
                    docker run -d --name node-app-%BUILD_NUMBER% -p %APP_PORT%:3000 %IMAGE_NAME%:%BUILD_NUMBER%
                '''
            }
        }
        stage('Verify'){
            steps{
                bat '''
                    echo APP Deployed Successfully
                    echo Open http://localhost:%APP_PORT%
                    docker ps
                '''
            }
        }
    }
}