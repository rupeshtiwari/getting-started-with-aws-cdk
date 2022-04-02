- [Getting Started with AWS CDK Infrastructure as Code](#getting-started-with-aws-cdk-infrastructure-as-code)
  - [Step 1: First time environment setup steps](#step-1-first-time-environment-setup-steps)
  - [Step 2: Create first AWS CDK project](#step-2-create-first-aws-cdk-project)
  - [Step 3: Synthesize an AWS CloudFormation template](#step-3-synthesize-an-aws-cloudformation-template)
  - [Step 4: Deploy the stack](#step-4-deploy-the-stack)
  - [Step 5: Modify the app](#step-5-modify-the-app)
  - [Step 6: Destroying the app's resources](#step-6-destroying-the-apps-resources)
  - [Reference](#reference)

# Getting Started with AWS CDK Infrastructure as Code

Learn how to write your first AWS CDK app in your laptop and deploy resources in your AWS account right from your laptop. I am using MAC os for this demo. Later on I will use `cloud9` to deploy resources in AWS cloud and try to setup CI/CD for my CDK app as well. I will try to setup CI/CD right from my GitHub repository also.

You CDK app has high level class called Stage. Stage can have many Stacks. You can synthesize ( convert code in cloudformation api ) & deploy one or more stacks to your AWS account. This tutorial walks you through creating and deploying a simple AWS CDK app, from initializing the project to deploying the resulting AWS CloudFormation template. The app contains one stack, which contains one resource: an Amazon S3 bucket.

We'll also show what happens when you make a change and re-deploy, and how to
clean up when you're done.

http://www.rupeshtiwari.com/getting-started-with-aws-cdk/

## Step 1: First time environment setup steps

1. Open `sudo vim ~/.aws/credentials` and set your access key and security key.
2. Install `aws-cdk` globally `npm i -g aws-cdk` check version `cdk --version`
   ![](https://i.imgur.com/1GLQ4HQ.png)
3. Run `aws sts get-caller-identity` to know your account number and run `aws configuration get region` to know your region
4. Run `cdk bootstrap aws://ACCOUNT-NUMBER/REGION`. Bootstrap AWS CDK that will create S3 container to store assets required for deployment.
   ![](https://i.imgur.com/hLKy41D.png)
5. If this is for production then make sure you create dedicated account to deploy your infrastructure and assign this account role to deploy on another accounts.
6. Install AWS toolkit extension in your VSCode that will help you to create, debug and deploy applications on AWS. You can also see all of your AWS CDK projects.
   ![](https://i.imgur.com/PnWnGYm.png)

## Step 2: Create first AWS CDK project

![](https://i.imgur.com/o8TqCRx.png)

1. Create the app
   ```
   mkdir hello-cdk
   cd hello-cdk
   ```
2. `cdk init app --language typescript`, it will create cdk template project also initialize git.
3. Build the app `npm run build`
4. `cdk ls` see stacks
5. Goto `lib/stack.ts` add below line
   ```ts
   // create new s3 bucket
   new s3.Bucket(this, 'CdkCreatedBucket', { versioned: true })
   ```

## Step 3: Synthesize an AWS CloudFormation template

Run `cdk synth`. The cdk synth generates a perfectly valid AWS CloudFormation template. You could take it and deploy it using the AWS CloudFormation console or another tool. But the AWS CDK Toolkit can also do that.
![](https://i.imgur.com/RCbSeON.png)


## Step 4: Deploy the stack

Run `cdk deploy`.  CDK will deploy the stack using AWS CloudFormation. The AWS CDK synthesizes your stack before each deployment. 

Cloudformation stack created at AWS account on my selected region. 
![](https://i.imgur.com/25xqzZV.png)


Deployment successful from my laptop 
![](https://i.imgur.com/B7M2zME.png)


S3 created in my AWS account hurray! 
![](https://i.imgur.com/Ad4Kkgt.png)

## Step 5: Modify the app
The AWS CDK can update your deployed resources after you modify your app. 
Update lib/hello-cdk-stack.ts.
```ts
new s3.Bucket(this, 'MyFirstBucket', {
  versioned: true,
  removalPolicy: cdk.RemovalPolicy.DESTROY,
  autoDeleteObjects: true
});
```

Run `cdk diff` to check the differences

 
![](https://i.imgur.com/qEim9xE.png)

Run `cdk deploy` to deploy changes. 

![](https://i.imgur.com/9Ru1jA3.png)

Before deploy S3 policy 

![](https://i.imgur.com/s5nQ9dh.png)


After deploy S3 policy changed 

![](https://i.imgur.com/YnjOwM1.png)

## Step 6: Destroying the app's resources
Now that you're done with the quick tour, destroy your app's resources to avoid incurring any costs from the bucket you created, as follows.

```
cdk destroy
```
Enter y to approve the changes and delete any stack resources.

![](https://i.imgur.com/S4WOpvE.png)

Destroy was super quick!! 

![](https://i.imgur.com/hGqoN5U.png)
## Reference

- https://docs.aws.amazon.com/cdk/v2/guide/getting_started.html
- https://docs.aws.amazon.com/cdk/v2/guide/hello_world.html
