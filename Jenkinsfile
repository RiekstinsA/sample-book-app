pipeline {
    agent any
    triggers { pollSCM('*/1 * * * *') }

    stages {
        stage('Install pip dependencies') {
            steps {
                script {
                    installPipDeps()
                }
            }
        }

        stage('Deploy to DEV') {
            steps {
                script {
                    deploy("dev", 1010)
                }
            }
        }

        stage('Tests on DEV') {
            steps {
                script {
                    test("dev")
                }
            }
        }

        stage('Deploy to STG') {
            steps {
                script {
                    deploy("staging", 2020)
                }
            }
        }

        stage('Tests on STG') {
            steps {
                script {
                    test("staging")
                }
            }
        }

        stage('Deploy to PREPROD') {
            steps {
                script {
                    deploy("preprod", 3030)
                }
            }
        }

        stage('Tests on PREPROD') {
            steps {
                script {
                    test("preprod")
                }
            }
        }

        stage('Deploy to PROD') {
            steps {
                script {
                    deploy("prod", 7004)
                }
            }
        }

        stage('Tests on PROD') {
            steps {
                script {
                    test("prod")
                }
            }
        }
    }
}

def installPipDeps() {
    echo "Cloning the repository and installing pip dependencies..."
    bat "git clone https://github.com/mtararujs/python-greetings"
    bat "dir"
    bat "pip install -r python-greetings/requirements.txt" 
}

def deploy(String environment, int port) {
    echo "Deploying to ${environment}..."
    bat "git clone https://github.com/mtararujs/python-greetings"
    bat "dir"
    bat "node_modules\\.bin\\pm2 delete \"greetings-app-${environment}\" || exit 0"
    bat "node_modules\\.bin\\pm2 start app.py --name greetings-app-${environment} --port ${port}"
}

def test(String environment) {
    echo "Running tests on ${environment}..."
    bat "git clone https://github.com/mtararujs/course-js-api-framework"
    bat "dir"
    bat "npm install"
    bat "npm run greetings greetings_${environment}"
}
