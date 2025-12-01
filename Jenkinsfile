pipeline {
    agent any

    tools {
        nodejs "Node18.16.0"
    }

    stages {
        stage('Clone Repo'){
            steps{
                script {
                    git branch: 'main',
                    url: 'https://github.com/widmert-bzz/firstJenkinsSteps.git'
                }
            }
        }
        stage('Install Jest'){
            steps{
                sh 'npm i jest-cli -g'
            }
        }
        stage('Install Dependencies'){
            steps{
                sh 'npm i'
            }
        }
        stage('Test'){
            steps{
                script {
                    // This block starts the app, waits for it, runs tests, and ensures the app stops
                    sh '''
                        node index.js &

                        APP_PID=$!

                        sleep 5

                        npm test || (kill $APP_PID && exit 1)

                        kill $APP_PID
                    '''
                }
            }
        }
    }
}