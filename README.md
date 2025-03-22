# Static Website CI/CD Pipeline

This repository contains the code and configuration for a CI/CD pipeline that deploys a static website to Amazon S3 using AWS CodePipeline and CodeBuild.

## Functionality

- **Source Stage:** Retrieves the website's source code from a GitHub repository.
- **Build Stage:** Builds the static website using AWS CodeBuild (or copies files directly if no build is needed).
- **Deploy Stage:** Deploys the built website files to an Amazon S3 bucket.

## Prerequisites

- An AWS account with appropriate permissions.
- An Amazon S3 bucket configured for static website hosting.
- A GitHub repository containing the static website files.
- AWS CodePipeline and CodeBuild configured.

## How to Use

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/BasitKhan-Cloud/aws-static-website-cicd.git](https://github.com/BasitKhan-Cloud/aws-static-website-cicd.git)
    ```

2.  **Configure AWS:**
    - Create an S3 bucket for your website.
    - Configure the bucket for static website hosting.
    - Create or use an existing IAM role with necessary permissions for CodePipeline and CodeBuild.
    - Create a CodePipeline pipeline using the AWS Management Console or AWS CLI, pointing to this repository.
    - Configure the CodeBuild stage to use the `buildspec.yml` file in the repository's root.

3.  **Make Changes:**
    - Modify the website files in the repository.
    - Commit and push the changes to your GitHub repository.

4.  **Automatic Deployment:**
    - CodePipeline will automatically trigger a new pipeline execution to build and deploy the updated website to S3.

## `buildspec.yml`

The `buildspec.yml` file in the root of the repository defines the build commands for CodeBuild.

```yaml
version: 0.2

phases:
  build:
    commands:
      - echo "Copying files to S3..."
artifacts:
  files:
    - '**/*'
  discard-paths: yes
