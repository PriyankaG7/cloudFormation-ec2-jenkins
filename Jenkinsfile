pipeline {
  agent any

  environment {
    AWS_REGION = 'us-east-2'
    S3_BUCKET = 'my-cloudformationtemplate-bucket7'
  }

  stages {
    stage('Authenticate with AWS') {
      steps {
        withCredentials([
          usernamePassword(
            credentialsId: 'aws-credentials',
            usernameVariable: 'AWS_ACCESS_KEY_ID',
            passwordVariable: 'AWS_SECRET_ACCESS_KEY'
          )
        ]) {
          sh '''
            aws sts get-caller-identity
            aws s3 ls
          '''
        }
      }
    }

    stage('Checkout') {
      steps {
        git url: 'https://github.com/PriyankaG7/cloudFormation-ec2-jenkins.git', branch: 'main'
      }
    }

    stage('Upload CloudFormation Template') {
      steps {
        sh 'aws s3 cp ec2.yml s3://my-cloudformationtemplate-bucket7/ec2.yml'
      }
    }

    stage('Deploy CloudFormation Stack') {
      steps {
        sh '''
          aws cloudformation create-stack \
             --stack-name MyWebServerStack \
             --template-body file://template1.yml \
             --parameters \
               ParameterKey=InstanceType,ParameterValue=t2.micro \
               ParameterKey=KeyName,ParameterValue=devops \
             --capabilities CAPABILITY_NAMED_IAM
        '''
      }
    }
  }
}