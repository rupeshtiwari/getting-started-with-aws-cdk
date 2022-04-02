- [Getting Started with AWS CDK Infrastructure as Code](#getting-started-with-aws-cdk-infrastructure-as-code)
  - [Step 1: First time environment setup steps](#step-1-first-time-environment-setup-steps)

# Getting Started with AWS CDK Infrastructure as Code 

## Step 1: First time environment setup steps
1. Open `sudo vim ~/.aws/credentials` and set your access key and security key. 
2. Install `aws-cdk` globally `npm i -g aws-cdk` check version `cdk --version`
   ![](https://i.imgur.com/1GLQ4HQ.png)
3. Run `aws sts get-caller-identity` to know your account number and run `aws configuration get region` to know your region
4. Run `cdk bootstrap aws://ACCOUNT-NUMBER/REGION`.  Bootstrap AWS CDK that will create S3 container to store assets required for deployment. 
   ![](https://i.imgur.com/hLKy41D.png)
