# aws-project

## Description
This project focuses on migrating Docker workloads to Amazon EKS, using Amazon ECR for container storage and implementing best practices for cloud-native infrastructure. It includes integration with Amazon SNS for notifications, AWS Secrets Manager for secure storage, and uses Jenkins in Kubernetes to automate CI/CD processes.

## Prerequisites
* AWS Account with permissions to access ECR, EKS, EC2, SNS, S3, and Secrets Manager.
* AWS CLI and kubectl installed and configured.
* Jenkins installed and accessible.

## Task 1: Migrate to ECR Private Repository
Create a private repository in Amazon ECR.
Push your existing container images to the ECR repository using the AWS CLI or AWS Management Console.
Set up access permissions for ECR to ensure Jenkins and Kubernetes can access the images.

## Task 2: Configure Jenkins Agent with EC2 
Set Up EC2 for Jenkins Agent:
Create an Amazon Machine Image (AMI) for the Jenkins agent with necessary dependencies.
Configure EC2 Fleet in Jenkins by adding it as a new cloud provider under Jenkins settings.
Parameterize Jenkinsfile:
Modify your Jenkinsfile to allow switching between Kubernetes pods and EC2 agents.
Use a parameter option like option(value: kubernetes-pods/ec2).

## Task 3: Backup EC2 Instances
For EC2 backup, select the instance to snapshot, provide a descriptive name, and ensure the configuration meets your requirements.

## Task 4: Host Static Website on S3
Create an S3 Bucket: Set up a bucket to host static files.
Upload Files: Upload HTML, CSS, JavaScript, and image files.
Enable Static Website Hosting: Configure bucket settings for static website hosting and specify an index document.

## Task 5: Migrate Jenkins to EKS
Create Namespaces:

Create namespaces with a prefix (e.g., <your name>-jenkins, <your name>-pollyapp, <your name>-argo).
Deploy Jenkins to EKS:

Deploy the Jenkins Helm chart in <your name>-jenkins namespace.
Transfer data from the existing Jenkins instance to EKS (e.g., /var/lib/jenkins).
Update Jenkins Pipelines:

Modify pipeline configurations to use Kubernetes agents in EKS for running CI/CD workloads.

## Task 6: Update Jenkinsfile for ECR Integration
Update your Jenkinsfile:
Modify image references to pull from ECR.
Test that Jenkins builds, deploys, and runs containers from the ECR repository.

## Task 7: Notifications with SNS
Install Amazon SNS Plugin:

Go to Manage Plugins in Jenkins and install the Amazon SNS Build Notifier plugin.
Create SNS Topic:

Create a new SNS topic in AWS for notifications.
Configure Jenkins for SNS:

Enter your AWS credentials under Jenkins system configuration.
Set up a post-build action to send an SNS notification with job details (job name, build number, build status).

## Task 8: clean up
Once migration is complete, clean up resources by:

Deleting the EC2 instances hosting Jenkins.
Removing any unused infrastructure from the Minikube cluster.

## Task 9: Secrets Management with AWS Secrets Manager
Install AWS Secrets and Configuration Provider:
Use the Secrets Store CSI Driver with AWS’s provider to mount Secrets Manager secrets in EKS.
Follow AWS documentation to mount Secrets Manager secrets as files in your EKS pods.

