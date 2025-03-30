pipeline {
    agent any

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
                    deploy("DEV")
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
                    deploy("STG")
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
                    deploy("PRD")
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

def deploy(String environment){
    echo "Deployment to ${environment} has started.."
}

def test(String environment){
    echo "Testing to ${environment} has started.."
}

def build(){
    echo "Building of node application is starting.."
}