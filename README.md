- [Getting Started with AWS CDK Infrastructure as Code](#getting-started-with-aws-cdk-infrastructure-as-code)
  - [Step 1: First time environment setup steps](#step-1-first-time-environment-setup-steps)
  - [Step 2: Create first AWS CDK project](#step-2-create-first-aws-cdk-project)

# Getting Started with AWS CDK Infrastructure as Code

Learn how to write your first AWS CDK app in your laptop and deploy resources in your AWS account right from your laptop. I am using MAC os for this demo. Later on I will use `cloud9` to deploy resources in AWS cloud and try to setup CI/CD for my CDK app as well. I will try to setup CI/CD right from my GitHub repository also. 

http://www.rupeshtiwari.com/getting-started-with-aws-cdk/

## Step 1: First time environment setup steps

1. Open `sudo vim ~/.aws/credentials` and set your access key and security key.
2. Install `aws-cdk` globally `npm i -g aws-cdk` check version `cdk --version`
   ![](https://i.imgur.com/1GLQ4HQ.png)
3. Run `aws sts get-caller-identity` to know your account number and run `aws configuration get region` to know your region
4. Run `cdk bootstrap aws://ACCOUNT-NUMBER/REGION`. Bootstrap AWS CDK that will create S3 container to store assets required for deployment.
   ![](https://i.imgur.com/hLKy41D.png)
5. If this is for production then make sure you create dedicated account to deploy your infrastructure and assign this account role to deploy on another accounts.

## Step 2: Create first AWS CDK project
