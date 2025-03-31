pipeline {
    agent any
    triggers { pollSCM('*/1 * * * *') }

    stages {
        stage('Install pip deps') {
            steps {
                script {
                    installDeps()
                }
            }
        }

        stage('Deploy to DEV') {
            steps {
                script {
                    deploy('dev', 7001)
                }
            }
        }

        stage('Tests on DEV') {
            steps {
                script {
                    test('dev')
                }
            }
        }

        stage('Deploy to STG') {
            steps {
                script {
                    deploy('staging', 7002)
                }
            }
        }

        stage('Tests on STG') {
            steps {
                script {
                    test('staging')
                }
            }
        }

        stage('Deploy to PREPROD') {
            steps {
                script {
                    deploy('preprod', 7003)
                }
            }
        }

        stage('Tests on PREPROD') {
            steps {
                script {
                    test('preprod')
                }
            }
        }

        stage('Deploy to PROD') {
            steps {
                script {
                    deploy('prod', 7004)
                }
            }
        }

        stage('Tests on PROD') {
            steps {
                script {
                    test('prod')
                }
            }
        }
    }
}

def installDeps() {
    echo "Cloning the repository and installing pip dependencies..."
    git url: 'https://github.com/RiekstinsA/python-greetings'
    bat "pip install -r requirements.txt"
}

def deploy(String environment, int port) {
    echo "Deployment to ${environment} has started.."
    git url: 'https://github.com/RiekstinsA/python-greetings'
    bat "pm2 delete greetings-app-${environment} & set errorlevel=0"
    bat "pm2 start app.py --name greetings-app-${environment} -- --port ${port}"
}

def test(String environment) {
    echo "Testing ${environment} environment.."
    git url: 'https://github.com/RiekstinsA/course-js-api-framework'
    bat "npm install"
    bat "npm run greetings greetings_${environment}"
}
