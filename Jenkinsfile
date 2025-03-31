pipeline {
    agent any
    triggers { pollSCM('*/1 * * * *') }

    stages {
        stage('Install pip dependencies') {
            steps {
                script {
                    echo "Cloning the repository and installing pip dependencies..."
                    installPipDeps()
                }
            }
        }

        stage('Deploy to DEV') {
            steps {
                script {
                    echo "Starting deployment to DEV environment..."
                    deploy("dev", 7001)
                }
            }
        }

        stage('Tests on DEV') {
            steps {
                script {
                    echo "Running tests on DEV environment..."
                    test("dev")
                }
            }
        }

        stage('Deploy to STG') {
            steps {
                script {
                    echo "Starting deployment to STG environment..."
                    deploy("staging", 7002)
                }
            }
        }

        stage('Tests on STG') {
            steps {
                script {
                    echo "Running tests on STG environment..."
                    test("staging")
                }
            }
        }

        stage('Deploy to PREPROD') {
            steps {
                script {
                    echo "Starting deployment to PREPROD environment..."
                    deploy("preprod", 7003)
                }
            }
        }

        stage('Tests on PREPROD') {
            steps {
                script {
                    echo "Running tests on PREPROD environment..."
                    test("preprod")
                }
            }
        }

        stage('Deploy to PROD') {
            steps {
                script {
                    echo "Starting deployment to PROD environment..."
                    deploy("prod", 7004)
                }
            }
        }

        stage('Tests on PROD') {
            steps {
                script {
                    echo "Running tests on PROD environment..."
                    test("prod")
                }
            }
        }
    }
}

def installPipDeps() {
    echo "Cloning the repository and installing pip dependencies..."
    bat "git clone https://github.com/RiekstinsA/python-greetings"
    bat "dir"
    bat "pip install -r python-greetings/requirements.txt"
}

def deploy(String environment, int port) {
    echo "Deploying to ${environment} environment..."
    bat "git clone https://github.com/RiekstinsA/python-greetings"
    bat "dir"
    bat "node_modules\\.bin\\pm2 delete \"greetings-app-${environment}\" || exit 0"
    bat "node_modules\\.bin\\pm2 start app.py --name greetings-app-${environment} --port ${port}"
}

def test(String environment) {
    echo "Running tests on ${environment} environment..."
    bat "git clone https://github.com/RiekstinsA/api-automation"
    bat "dir"
    bat "npm install"
    bat "npm run greetings greetings_${environment}"
}
