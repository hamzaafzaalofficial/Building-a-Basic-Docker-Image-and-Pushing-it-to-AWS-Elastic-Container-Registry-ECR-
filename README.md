# Building-a-Basic-Docker-Image-and-Pushing-it-to-AWS-Elastic-Container-Registry-ECR-


# Task 1: Install Docker
If you haven't already, install Docker on your local machine. You can download it from the official docker website. 





Pre-Requisites: 

sudo snap install aws-cli --classic 
aws --version



#Creating an IAM user:

#Go to IAM Services and create a user, when attaching a policy add to #AmazonEC2ContainerRegistryFullAccess and click create and download the user-#credentials.

#Then create a secret key, and download the access key ID and Secret access key 
#Access key ID   AKIeeLQFE3KHS7ggee
#Secret access key  7eeNeeVapKTyza5neehLee3jUvA44in


aws configure 
#it will prompt you to enter the access key ID and secret access key, you have to #enter these values as generated for the both above for the iam user. See the #advantage of using IAM user, is the least priviledge concept. 
#It will further prompt for region, enter your region, mine was us-east-1
#and enter the output form as : json


# Task 2: Create a Dockerfile
Create a file called Dockerfile in your project directory. This file defines how your Docker image should be built:

# Use an official Nginx base image
FROM nginx:latest

# Copy your code and any other static files to the container
COPY . /usr/share/nginx/html

# Expose port 8080 to listen for incoming HTTP requests
EXPOSE 8080

# Start Nginx when the container starts
CMD ["nginx", "-g", "daemon off;"]


# Task 3: Create an ECR Repository
If you haven't already, create a repository in AWS ECR to store your Docker image. You can do this through the AWS Management Console or using the AWS CLI.



When you create the repo, you should see some push commands. Following down, we will use them to push image to ECR. 

# Task 4: Authenticate to AWS ECR
Before you can push the image to AWS ECR, you need to authenticate your Docker client with your AWS account:



aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.<your-region>.amazonaws.com




sudo usermod -aG docker $USER


# Task 5: Build the Docker Image
Open a terminal in your project directory and run the following command to build your Docker image:



docker build -t test1 .




# Task 6: Tag the Docker Image

Tag your Docker image with the ECR repository URI:



docker tag test1:latest 780621109903.dkr.ecr.us-east-1.amazonaws.com/test1:latest


# Task 7: Push the Docker Image to ECR


Push the Docker image to AWS ECR using the following command:



docker push 780621109903.dkr.ecr.us-east-1.amazonaws.com/test1:latest


















