#!/usr/bin/env groovy
pipeline {
    agent any

    stages {
        stage('Install-pip-deps') {
            steps {
                echo 'Installing all required dependencies...'
                git url: 'https://github.com/mtararujs/python-greetings', branch: 'main'
                bat 'dir' // Windows: failu saraksts
                bat '"C:\\Users\\davis\AppData\\Local\\Programs\\Python\\Python313\\Scripts\\pip.exe" install -r requirements.txt'
            }
        }
        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to dev...'
                git url: 'https://github.com/mtararujs/python-greetings', branch: 'main'
                bat 'pm2 delete greetings-app-dev & set "errorlevel%l=0"' // Windows: pm2 delete
                bat 'pm2 start app.py --name greetings-app-dev --port 7001'
            }
        }
        stage('tests-on-dev') {
            steps {
                echo 'Running tests on dev...'
                git url: 'https://github.com/mtararujs/course-js-api-framework', branch: 'main'
                bat 'npm install'
                bat 'npm run greetings greetings_dev'
            }
        }
        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging...'
                git url: 'https://github.com/mtararujs/python-greetings', branch: 'main'
                bat 'pm2 delete greetings-app-staging & set "errorlevel%l=0"' // Windows: pm2 delete
                bat 'pm2 start app.py --name greetings-app-staging --port 7002'
            }
        }
        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging...'
                git url: 'https://github.com/mtararujs/course-js-api-framework', branch: 'main'
                bat 'npm install'
                bat 'npm run greetings greetings_staging'
            }
        }
        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to preprod...'
                git url: 'https://github.com/mtararujs/python-greetings', branch: 'main'
                bat 'pm2 delete greetings-app-preprod & set "errorlevel%l=0"' // Windows: pm2 delete
                bat 'pm2 start app.py --name greetings-app-preprod --port 7003'
            }
        }
        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on preprod...'
                git url: 'https://github.com/mtararujs/course-js-api-framework', branch: 'main'
                bat 'npm install'
                bat 'npm run greetings greetings_preprod'
            }
        }
        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to prod...'
                git url: 'https://github.com/mtararujs/python-greetings', branch: 'main'
                bat 'pm2 delete greetings-app-prod & set "errorlevel%l=0"' // Windows: pm2 delete
                bat 'pm2 start app.py --name greetings-app-prod --port 7004'
            }
        }
        stage('tests-on-prod') {
            steps {
                echo 'Running tests on prod...'
                git url: 'https://github.com/mtararujs/course-js-api-framework', branch: 'main'
                bat 'npm install'
                bat 'npm run greetings greetings_prod'
            }
        }
    }
}
