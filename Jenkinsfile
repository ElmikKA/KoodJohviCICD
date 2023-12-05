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
        stage("build application"){
            steps {
                echo 'Building application'
                sh 'npm run build'
            }
        }
        stage("all of the stuff"){
            steps {
              script {
                def branchNames = env.BRANCH_NAME

                sh 'mkdir -p /kj_deployments/kelmik_${branchNames}'
                sh 'cp -r * /kj_deployments/kelmik_${branchNames}'
                sh 'mv /kj_deployments/kelmik_${branchNames}/src/index.html /kj_deployments/kelmik_${branchNames}/index.html'
              }
                
            }
        }
    }
}
