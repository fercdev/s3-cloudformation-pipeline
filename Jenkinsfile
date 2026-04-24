pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'
        STACK_NAME = 'stack-s3-static-website'
    }

    stages {
        stage('Validate Cli veresion') {
            steps {
                withAWS(credentials: 'aws-credentials', region: "${AWS_REGION}") {
                    sh 'aws --version'
                }
            }
        }


        stage('Deploy CloudFormation (Create Bucket)') {
            steps {
                withAWS(credentials: 'aws-credentials', region: "${AWS_REGION}") {
                    sh '''
                    aws cloudformation deploy \
                      --template-file cloudformation/s3-bucket.yaml \
                      --stack-name ${STACK_NAME} \
                      --capabilities CAPABILITY_NAMED_IAM
                    '''
                }
            }
        }
    }
}