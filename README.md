# MERN Stack Blog App Deployment
This assignment involves deploying a full-stack MERN (MongoDB, Express.js, React.js, Node.js) blog application on AWS. The primary objective is to automate the infrastructure setup and application deployment process using Terraform and Ansible. This includes:

-   Provisioning an EC2 instance for the backend server.
-   Configuring MongoDB Atlas for the database.
-   Setting up S3 buckets for frontend hosting and media uploads.
-   Ensuring secure access and proper configuration of all components.

## Steps

1.  **Infrastructure Setup with Terraform:**
    * Defined the required AWS resources (EC2 instance, security groups, S3 buckets) using Terraform.
    * Created an IAM user and policy for secure S3 access for media uploads.
    * Configured the EC2 instance with a Launch Template, specifying the Ubuntu 22.04 AMI and security group.
2.  **MongoDB Atlas Configuration:**
    * Created a free-tier MongoDB Atlas cluster.
    * Whitelisted the EC2 instance's IP address to allow database connections.
    * Created a database user and obtained the connection string.
    * (The connection string is used in the backend application's `.env` file).
3.  **Backend Deployment with Ansible:**
    * Used Ansible to automate the backend server setup on the EC2 instance.
    * The Ansible playbook выполняет следующие действия:
        * Cloned the blog application repository from GitHub.
        * Generated and configured the `.env` file with MongoDB Atlas and S3 credentials.
        * Installed dependencies using `npm install`.
        * Started the backend server using PM2 for process management.
4.  **Frontend Deployment to S3:**
    * Configured an S3 bucket to host the static files of the React frontend application.
    * Enabled static website hosting for the S3 bucket.
    * Uploaded the built frontend files to the S3 bucket using the AWS CLI.
5.  **Media Uploads Configuration:**
    * Configured an S3 bucket to store media files uploaded through the application.
    * Applied a CORS policy to the media bucket to allow uploads from the frontend.
    * The backend application is configured to handle media uploads to this S3 bucket using the IAM user credentials.

## Tools/Services Used

* **Terraform:** Infrastructure as Code (IaC) tool for provisioning AWS resources.
* **Ansible:** Automation tool for configuring the EC2 instance and deploying the backend application.
* **AWS:**
    * EC2: Virtual server for running the backend application.
    * S3: Storage service for hosting the frontend and storing media uploads.
    * IAM: Identity and Access Management for managing access to AWS resources.
* **MongoDB Atlas:** Cloud database service for storing the application's data.

## Cleanup Steps

To clean up the deployed resources:

1.  Use `terraform destroy` to delete all AWS resources created by Terraform (EC2 instance, S3 buckets, etc.).
2.  Manually delete any resources created outside of Terraform (if any).
3.  Remove any sensitive credentials or `.env` files from the EC2 instance.
4.  Delete any manually created MongoDB Atlas users or IP access rules.
5.  Revoke or delete the IAM user credentials created for S3 access.

## Screenshots

The following screenshots demonstrate the successful deployment of the application:

* `pm2-backend.png`: PM2 process showing the backend server running.
* `mongodb-cluster.png`: MongoDB Atlas cluster dashboard.
* `media-upload-success.png`: A blog post image successfully uploaded and visible.
* `s3-frontend.png`: The frontend application running in the browser via the S3 static site URL.
