pipeline {
    agent any

    stages{
        stage('Build Frontend'){
            steps{
                sh "echo Building Frontend"
                sh "cd frontend && npm install && npm run build"
            }
        }

        stage('Deploy Frontend'){
            steps{
                script{
                    withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS'){
                        sh "aws sync frontend/dist s3://boardgame-inventory-management"
                    }
                }
            }
        }
    }
}
