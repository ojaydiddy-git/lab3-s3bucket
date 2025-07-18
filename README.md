Lab 3: Deploy Infrastructure Using AWS CodePipeline and CloudFormation
This lab demonstrates how to automate the deployment of an AWS S3 bucket using AWS CodePipeline integrated with GitHub and CloudFormation.
✅ Lab Objectives
•	• Connect GitHub repository to CodePipeline.
•	• Deploy an S3 bucket using a CloudFormation template.
•	• Use parameter overrides to pass dynamic values to CloudFormation.
•	• Confirm auto-trigger on GitHub commit.
🧱 Step-by-Step Summary
1. Create CloudFormation Template
File: cloudformation-s3.yml
Defines an S3 bucket with parameterized name:
Parameters:
  BucketName:
    Type: String
Resources:
  S3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Ref BucketName

2. Initialize GitHub Repository
Create a GitHub repo and push the CloudFormation template:
git init
git remote add origin https://github.com/<your-username>/lab3-s3bucket
git add cloudformation-s3.yml
git commit -m "Add S3 bucket template"
git push -u origin main

3. Create AWS CodePipeline
Stages:
•	• Source: Connect to GitHub (via GitHub App)
•	• Deploy: Use AWS CloudFormation
Set the template file to: cloudformation-s3.yml
Define the stack name: MyS3Stack
Assign the appropriate IAM execution role
4. Pass Parameter to CloudFormation
In the Deploy stage, under Advanced > Parameter overrides, add:
{
  "BucketName": "my-lab3-bucket-<your-id>"
}

5. Trigger Deployment
Save and release the pipeline.
Confirm S3 bucket is created via AWS Console.
6. Test Auto-Trigger
Make a small change to cloudformation-s3.yml or add a new file.
Push the change to GitHub.
Verify the pipeline auto-triggers and redeploys.
📌 Final Notes
•	• Ensure the CodePipeline role has iam:PassRole and cloudformation:CreateStack permissions.
•	• Use globally unique bucket names to avoid deployment failures.
•	• Check CloudFormation and CodePipeline logs for troubleshooting.
✅ Outcome
An automated CI/CD pipeline that deploys an S3 bucket from GitHub using AWS CodePipeline and CloudFormation.
