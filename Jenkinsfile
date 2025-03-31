pipeline {
    agent any

    stages {
        stage('Install-pip-deps') {
            steps {
                script {
                    installPipDeps()
                }
            }
        }
        stage('Deploy to DEV') {
            steps {
                script {
                    deploy("DEV", 7001)
                }
            }
        }
        stage('Tests on DEV') {
            steps {
                script {
                    testing("DEV")
                }
            }
        }
        stage('Deploy to STG') {
            steps {
                script {
                    deploy("STG", 7002)
                }
            }
        }
        stage('Tests on STG') {
            steps {
                script {
                    testing("STG")
                }
            }
        }
        stage('Deploy to PRD') {
            steps {
                script {
                    deploy("PRD", 7004)
                }
            }
        }
         stage('Tests on PRD') {
            steps {
                script {
                    testing("PRD")
                }
            }
        }
    }
}

def installPipDeps(){
    echo "Installing Python dependencies"
    git 'https://github.com/mtararujs/python-greetings'
    sh 'pip install -r requirements.txt'
}

def deploy(String environment, int port) {
    echo "Deploying to ${environment}"
    git 'https://github.com/mtararujs/python-greetings'
    // Windows komanda
    //sh "pm2 delete greetings-app-${environment} & set \"errorlevel%l=0\""
    // Unix komanda
    sh "pm2 delete greetings-app-${environment} || true"
    sh "pm2 start app.py --name greetings-app-${environment} --port ${port}"
}

def testing(String environment) {
    echo "Testing on ${environment}"
    git 'https://github.com/mtararujs/course-js-api-framework'
    sh 'npm install'
    sh "npm run greetings greetings_${environment}"
}
