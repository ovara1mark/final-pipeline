# Purpose of This Repo

This repos has a sample "Hello World" flask application that we will deploy on EKS cluster using the AWS Codebuild and Codepipeline services. 
Here is the purpose of each file present in this repo:
```bash

├── app.py         # A sample "Hello World" flask application
├── ci-cd-codepipeline.cfn.yml # Cloudformation template to create the Codebuild, and Codepipeline, and related resources. 
├── buildspec.yml  # Codebuild will execute the commands available here. 
├── Dockerfile     # Codebuild will build an image using the Dockerfile, and push it to the Dockerhub/or AWS ECR. 
├── deployment.yml # The deployment file for the Kubernetes cluster. Codebuild will apply this deployment using the one of the kubectl commands.   
├── iam-role-policy.json # The Policy for the IAM role that the Codebuild will assume
├── trust.json # The trusted entity details for the  IAM role that the COdebuild will assume
└── aws-auth-patch.yml  # This is an autogenerated file for your reference. 
```



## Run the app on AWS Cloud
The steps you will follow are:
1. **Create an EKS Cluster, IAM Role for CodeBuild, and Authenticate the CodeBuild**<br>
You will start with creating an EKS cluster in your preferred region, using `eksctl` command. Then, you will create an IAM role that the Codebuild will assume to access your k8s/EKS cluster. This IAM role will have the necessary access permissions (attached JSON policies), and you will also have to add this role to the k8s cluster's configMap. <br><br>


2. **Deployment to Kubernetes using CodePipeline and CodeBuild**
 - **Generate a Github access token**<br>Next, you will generate an access-token from your Github account so that whichever service has that token can access the repositories from your Github account. You will share this token with the AWS Codebuild service (programmatically) so that it can build and test your code. <br><br>
 
 - **Create Codebuild and CodePipeline resources using CloudFormation template**<br>Create a pipeline watching for commits to your Github repository. You will create the necessary AWS resources using a script, Cloudformation template (.yaml) file, available to you. These resources collectively are called **stack**. It will automatically create the Codebuild and Codepipeline projects for you. <br><br>
 
 
 - **Build and deploy**<br>Finally, you will trigger the **build** based on a Github commit. 
# final-pipeline
