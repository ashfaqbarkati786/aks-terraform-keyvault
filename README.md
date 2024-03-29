# Platform Engineering on AWS for Data Analytics Projects

# Table of Contents

- [Introduction](#introduction)
- [Project Overview](#project-overview)
  - [What is this project?](#what-is-this-project)
  - [Why do we need this?](#why-do-we-need-this)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
  - [Project Architecture](#project-architecture)
- [Folder Structure](#folder-structure)
- [Change Management](#change-management)
- [CI/CD Process](#cicd-process)
- [Source File Location](#source-file-location)
- [Destination File Location](#destination-file-location)
- [Usage](#usage)



## Introduction:

Welcome to "Platform Engineering on AWS for the Data Analytics Project." This initiative serves as a comprehensive toolkit, facilitating the deployment of infrastructure resources through Terraform modules and the execution of ETL (Extract, Transform, Load) operations using a Python script.

## Project Overview:

### What is this Project?

This project aims to design and implement end-to-end DevOps tooling and methodologies for data engineering and analytics. We aim to streamline the data processing workflow and ensure efficient deployment and monitoring of data-related applications, thereby achieving amalgamation of Data and DevOps also known as DataOps.

### Why Do We Need This?

The project addresses the complexities of data processing, ensuring high-quality insights and accelerating time-to-insight. By streamlining operations, optimizing costs, and enhancing security and compliance, it aligns with our strategic goals and promotes efficient resource management. Proactive monitoring and governance policies further enhance reliability and scalability, empowering us to handle evolving data demands effectively.

- To enhance our operational footprint across diverse cloud providers such as AWS and establish a cloud-agnostic solution for implementing data engineering and analytics projects.
- Helpful for Cervello/Kearney future projects in analyzing and identifying the right services/tools from AWS based on advantages and drawbacks.
- Terraform modules that are project-ready, ensuring they are reusable in new projects.

## Prerequisites 

To make use of this project, ensure the following requirements are met: 

- AWS account with the required policies and permissions to access the project resources.
- AWS CLI should be installed and configured with the appropriate credentials. 
- Git should be installed on your local machine for repository interactions. 

## Project Structure 
The project is structured as follows: 
- The data transformation script and Terraform module for infrastructure deployment have been pushed to the AWS Code Commit repository.
- **Code Build:** Code Build is employed to create an agent with specific requirements, facilitating the initiation of Terraform deployment.  
- **Code Pipeline:** AWS Code Pipeline for orchestrating the data ops pipeline. 
- **Glue:** AWS Glue for data transformation jobs. 
- **Lambda:** Lambda functions are used to automate the process of initiating the AWS Crawler and AWS ETL Job using S3 and CloudWatch events.
- **Cloud Watch:** Monitoring and logging for the entire pipeline and for services like Glue Crawler, Glue Job, Lambda functions, VPC, Glue connection & Code Commit. 
- **SNS:** Simple Notification Service for handling notifications. 
- **S3:** Storage for input datasets, ETL script and transformed output data.
### Project Architecture
![image](https://github.com/ashfaqbarkati786/aks-terraform-keyvault/assets/107784646/bfbaa441-94ec-4f4d-868c-3c4375bc0377)


## Folder Structure
- **`Deployments`**: Repository
  - **`dev/`**: Development environment directory.
    - **`output.tf`**: Terraform file providing outputs for the resources.
    - **`provider.tf`**: Terraform file defining the cloud provider used for deployment.
    - **`variable.tf`**: Terraform file defining variables utilized in the `main.tf` file.
    - **`backend.tf`**: Terraform file containing code to centralize the state files.
    - **`main.tf`**: Main Terraform file responsible for orchestrating deployments and creating the infrastructure.
      
  - **`files/`**: directory.
    - `python.py`: Python file for ETL transformation operations that may be used across environments.

  - **`prod/`**: Production environment directory.
    - **`output.tf`**
    - **`provider.tf`**
    - **`variable.tf`**
    - **`backend.tf`**
    - **`main.tf`**
      

## Change Management

- To make any changes to ETL script or IaC code in the Production environment, a Pull request has to be raised and should be approved by Architects/SME’s to promote changes.
- To deploy the new changes in Dev or Production environment, the pipeline should be approved by Architects/SME’s before applying the infrastructure changes.

## CI/CD Process

The project follows a continuous integration and continuous deployment (CI/CD) process. When changes are pushed to the Code Commit repository, the CI/CD pipeline is triggered. The pipeline includes the following stages: 

- **Source:** Monitors the Code Commit '**deployments**' repository for changes. 
- **Build:** Leverage AWS CodeBuild for building the build specification file, and incorporate an agent for deploying Terraform modules to create the necessary infrastructure.
- **Deploy:** Upload the processed dataset to the designated output Amazon S3 bucket. This involves placing the data that has undergone transformation, originally uploaded for processing, into the specified storage location within the Amazon S3 service.
- **Notification:** Sends notifications via SNS to email service for successful or failed pipeline execution.

### CI/CD Architecture
![image](https://github.com/ashfaqbarkati786/aks-terraform-keyvault/assets/107784646/cff6aea5-e00b-4e0c-b696-96bc806a3f81) 
**legend**
 1. AWS CodeCommit  is a Version Control Service hosted by AWS, to store the Terraform code. This is similar to Github
 2. AWS codepipline : AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates.
 3. Buildspec File : A buildspec is a collection of build commands and related settings, in YAML format, that CodeBuild uses to run a build.
 4. AWS Codebuild : AWS CodeBuild is a fully managed continuous integration service that compiles source code, runs tests, and produces ready-to-deploy software packages.
 5. Resources : After the pipeline execution,Terraform have deployed this resources per envirenment.
 6. After successfull deployment in the dev environment we will be promoting the changes to prod environment having Manual approval in place.
 7. TF State Files : We are storing the Terraform statefiles to S3 bucket

## Source File Location 

The initial datasets for processing are stored in the specified input S3 bucket as defined in the project configuration. Access the input files at `s3://path_to_directory/input/`.  

## Destination File Location 

The transformed data is stored in the output S3 bucket specified in the project configuration. You can find the output files at `s3://path_to_directory/output/`. 

## Usage 

To use this project for your needs: 

1. **Clone the CodeCommit Repository:**
   - Repository URL: Retrieve the repository URL from the AWS CodeCommit console.
   - Git Clone: Clone the repository to your local environment using `git clone codecommit://profile-name@repo-name`.

2. **Deploy Infrastructure via Terraform:**
   - Terraform Configuration: Ensure Terraform modules for infrastructure are correctly configured and modified as per requirements.
   - Pipeline Trigger: Set up AWS Code Pipeline to deploy the infrastructure.
   - Version Control: Utilize Git for version control. Commit and push your data transformation scripts to the Code Commit repository.

3. **Upload Dataset to Input S3 Bucket:**
   - AWS Console Upload: Use the AWS console to upload datasets to the specified input S3 bucket.

4. **Retrieve Transformed Data:**
   - S3 Console: Navigate to the AWS S3 console. Access the specified output S3 bucket at `s3://path_to_directory/output/`.

5. **Data Validation:**
   - Validate the transformed data to ensure it meets expected criteria.

6. **Download Options:**
   - Download transformed data using the AWS CLI or S3 console.

7. **Monitor Pipeline Progress:**
   - AWS Code Pipeline Console: Monitor the progress of each stage in the pipeline, including source, build, deploy, etc.
   - CloudWatch Logs: Review CloudWatch logs for detailed information on each pipeline execution.

For any issues or errors, refer to the logs in CloudWatch and set up notifications through SNS for timely updates. Feel free to customize the pipeline stages, Glue jobs, and Lambda functions to suit your specific data transformation requirements.
