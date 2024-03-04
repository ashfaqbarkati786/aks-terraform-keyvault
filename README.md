Platform Engineering on AWS 
for Data Analytics Projects

Introduction:

Welcome to "Platform Engineering on AWS for the Data Analytics Project". This initiative serves as a comprehensive toolkit, facilitating the deployment of infrastructure resources through Terraform modules and the execution of ETL (Extract, Transform, Load) operations using a Python script.


Project Overview:

What is this Project?

This project aims to automate the data flow by implementing end-to-end DevOps tooling and methodologies within the AWS cloud for data engineering and analytic projects.

Why Do We Need This?
The project is addressing the complexities of data processing, ensuring high-quality insights, and accelerating time-to-insight. By streamlining operations, optimizing costs, and enhancing security and compliance, it aligns with our strategic goals and promote efficient resource management. Proactive monitoring and governance policies further enhance reliability and scalability, empowering us to handle evolving data demands effectively.

•	To enhance our operational footprint across diverse cloud providers such as AWS and establish a cloud-agnostic solution for implementing data engineering and analytics projects.
•	This will be helpful for future projects in analyzing and identifying the right services/tools from AWS based on advantages and drawbacks.
•	Terraform modules that are project-ready, ensuring they are reusable in new projects.

Prerequisites 

To make use of this project, ensure the following requirements are met: 

•	AWS account with the required policies and permissions to access the project resources.
•	AWS CLI should be installed and configured with the appropriate credentials. 
•	Git should be installed on your local machine for repository interactions. 




Project Structure 
 
The project is structured as follows: 
•	The data transformation script and Terraform module for infrastructure deployment have been pushed to the AWS Code Commit repository.
•	Code Build: Code Build is employed to create an agent with specific requirements, facilitating the initiation of Terraform deployment.  
•	Code Pipeline: AWS Code Pipeline for orchestrating the data ops pipeline. 
•	Glue: AWS Glue for data transformation jobs. 
•	Lambda: Lambda functions are used to automate the process of initiating the AWS Crawler and AWS ETL Job using S3 and CloudWatch events.
•	Cloud Watch: Monitoring and logging for the entire pipeline and for services like Glue Crawler, Glue Job, Lambda functions, VPC, Glue connection & Code Commit. 
•	SNS: Simple Notification Service for handling notifications. 
•	S3: Storage for input datasets, ETL script and transformed output data. 

Change management

•	To make any changes to ETL script or IaC code in the Production environment, a Pull request has to be raised and should be approved by Architects/SME’s promote changes.

•	To deploy the new changes in Dev or Production environment, the pipeline should be approved the Architects/SME’s changes before applying the infrastructure changes.

CI/CD Process
The project follows a continuous integration and continuous deployment (CI/CD) process. When changes are pushed to the Code Commit repository, the CI/CD pipeline is triggered. The pipeline includes the following stages: 
·	Source: Monitors the Code Commit repository for changes. 
·	Build: Uses Code Build to build and package the code. 
·	Deploy: Moves the transformed data to the output S3 bucket. 
·	Notification: Sends notifications via SNS for successful or failed pipeline execution.

Input File Location 
The initial datasets for processing are stored in the specified input S3 bucket as defined in the project configuration. Access the input files at “s3://path_to_directory/input/”.  
 
Output File Location 
The transformed data is stored in the output S3 bucket specified in the project configuration. You can find the output files at “s3://path_to_diretory/output/”. 
 
 
Usage 
To use this project for your needs: 
Clone the CodeCommit Repository:
Repository URL:
•	Retrieve the repository URL from the AWS CodeCommit console.
Git Clone:
•	Clone the repository to your local environment.
•	git clone codecommit://profile-name@repo-name 
Deploy Infrastructure via Terraform:
Terraform Configuration:
•	Ensure Terraform modules for infrastructure are correctly configured and modified as per requirement.
Pipeline Trigger:
•	Set up AWS Code Pipeline to deploy the infrastructure.
Version Control:
•	Utilize Git for version control.
•	Commit and push your data transformation scripts to the Code Commit repository:
Upload Dataset to Input S3 Bucket:
AWS Console Upload:
•	Use the AWS console to upload datasets to the specified input S3 bucket:
Retrieve Transformed Data:
S3 Console:
•	Navigate to the AWS S3 console.
•	Access the specified output S3 bucket at s3://path_to_directory/output/.
Data Validation:
•	Validate the transformed data to ensure it meets expected criteria.
Download Options:
•	Download transformed data using the AWS CLI or S3 console:
Monitor Pipeline Progress:
AWS Code Pipeline Console:
•	Monitor the progress of each stage in the pipeline, including source, build, deploy, etc.
CloudWatch Logs:
•	Review CloudWatch logs for detailed information on each pipeline execution.

For any issues or errors, refer to the logs in CloudWatch and set up notifications through SNS for timely updates. 
Feel free to customize the pipeline stages, Glue jobs, and Lambda functions to suit your specific data transformation requirements. 
 



![image](https://github.com/ashfaqbarkati786/aks-terraform-keyvault/assets/107784646/54381b8f-754d-457c-9870-0ea62b7be5a3)
