pipeline {
    agent any
    triggers{ pollSCM('*/1 * * * *') }

    stages {
        stage('Build') {
            steps {
                script{
                    build()
                }
            }
        }
        stage('Deploy to DEV') {
            steps {
                script{
                    deploy("DEV", 1010)
                }
            }
        }
        stage('Tests on DEV') {
            steps {
                script{
                    test("DEV")
                }
            }
        }
        stage('Deploy to STG') {
            steps {
                script{
                    deploy("STG", 2020)
                }
            }
        }
        stage('Tests on STG') {
            steps {
                script{
                    test("STG")
                }
            }
        }
        stage('Deploy to PRD') {
            steps{  
                script{
                    deploy("PRD", 3030)
                }
            }
        }
        stage('Tests on PRD') {
            steps {
                script{
                    test("PRD")
                }
            }
        }
    }
}

 def build(){
    echo "Building of node application is starting.."
    // bat "dir"
    // bat "npm install"
}
 
 def deploy(String environment, int port){
    echo "Deployment to ${environment} has started.."
    // git branch: 'jenkins_pipeline_windows', poll: false, url: 'https://github.com/RiekstinsA/sample-book-app.git'
    // bat "npm install"
    // bat "dir"
    bat "node_modules\\.bin\\pm2 delete \"books-${environment}\" || exit 0"
    bat "node_modules\\.bin\\pm2 start -n \"books-${environment}\" index.js -- ${port}"
 }

def test(String environment){
    echo "Testing to ${environment} has started.."
}