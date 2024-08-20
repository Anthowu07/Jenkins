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
                    try{
                        withAWS(region: 'us-east-1', credentials: 'AWS_CREDENTIALS'){
                            sh "aws s3 sync frontend/dist s3://boardgame-inventory-management"
                            //sh "aws elasticbeanstalk create-application-version --application-name myName --version-label your-version-label 0.0.1 --source-bundle S3Bucket="boardgame-inventory-management",S3Key="*.jar""
                            //sh "aws elasticbeanstalk update-environment --environment-name myName --version-label your-version-label"
                        }
                    }catch(Exception e){
                        echo "${e}"
                        throw e
                    }
                }
            }
        }

        stage('Build Backend'){
            steps{
                sh "cd demo && mvn clean install"
            }
        }

        stage('Test Backend'){
            steps{
                sh "cd demo && mvn test"
            }
        }
    }
}
