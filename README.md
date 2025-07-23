# cloudFormation-ec2-jenkins
Creating Jenkins-pipeline using Cloud Formation Template
# CloudFormation EC2 Deployment with Jenkins CI/CD

This project uses Jenkins to deploy an EC2 web server via CloudFormation.

## 🔧 Files

- `template1.yml` – Root CloudFormation template
- `ec2.yml` – Nested EC2 instance template
- `parameter.yml` – Parameter values
- `Jenkinsfile` – CI/CD pipeline to deploy
- `Jenkinsfile-destroy` – Pipeline to destroy the stack

## 📦 Setup

1. Create an S3 bucket:  
   `aws s3 mb s3://my-cloudformationtemplate-bucket`

2. Replace the S3 bucket name in `template1.yml` and `Jenkinsfile`.

3. Add your EC2 KeyPair name in `parameter.yml`.

## 🚀 Deploy via Jenkins

- Run the `Jenkinsfile` pipeline to deploy the EC2 stack.

## 🗑️ Destroy via Jenkins

- Run the `Jenkinsfile-destroy` pipeline to delete the CloudFormation stack and EC2 instance.

## 📝 Requirements

- AWS CLI installed and configured
- IAM user with `cloudformation:*`, `s3:*`, and `ec2:*` permissions
- Jenkins installed with Git and Shell plugins