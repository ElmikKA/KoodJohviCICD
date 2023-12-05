pipeline {
    agent any
    tools {
         nodejs 'nodejs21'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ElmikKA/KoodJohviCICD.git'
            }
        }
        stage("npm install") {
            steps {
                echo 'Npm installed'
                sh 'npm install'
            }
        }

        stage("Build Application") {
            steps {
                echo 'Building application'
                sh 'npm run build'
            }
        }

        stage("Build and Push Container") {
            steps {
                script {
                    def branchName = env.BRANCH_NAME
                    def dockerImageTag = "kj_deployments/kelmik/${branchName}:latest"

                    catchError {
                        // Build Docker image
                        sh "docker build -t ${dockerImageTag} ."

                      //Run container
                      sh "docker run -p 3000:3000 ${dockerImageTag}"
                    }
                }
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed!'
        }
    }
}
