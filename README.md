This project is a web application hosted on AWS S3 and deployed using AWS CodePipeline. The purpose of this project is to demonstrate how to automate the deployment process from a GitHub repository to an S3 bucket without needing IAM roles.

## Prerequisites

Before you begin, ensure you have the following:

- **AWS Account**: You need an AWS account to create resources such as S3 buckets and CodePipeline.
- **GitHub Account**: Your code should be hosted on GitHub.
- **AWS CLI**: Install the AWS CLI to interact with AWS services from the command line.
- **Personal Access Token**: Generate a GitHub personal access token with the necessary repository permissions.

## Setup Instructions

### 1. Create an S3 Bucket

Create an S3 bucket to host your static site.

```bash
aws s3 mb s3://your-bucket-name --region your-region
```

Enable public access and static website hosting on the S3 bucket.

```bash
aws s3 website s3://your-bucket-name/ --index-document index.html
```

### 2. Push Your Code to GitHub

Ensure your code is in a GitHub repository. If you haven't pushed it yet:

```bash
git init
git remote add origin https://github.com/yourusername/your-repo.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

### 3. Set Up AWS CodePipeline

1. **Create a Pipeline**:
   - Go to the AWS Management Console.
   - Navigate to **CodePipeline**.
   - Click on **Create Pipeline**.

2. **Configure the Pipeline**:
   - **Source Provider**: Select **GitHub**.
   - **Authentication**: Use your GitHub personal access token to authenticate.
   - Choose your repository and branch.

3. **Build Stage**:
   - If your project requires a build process (e.g., compiling assets), configure a build stage using AWS CodeBuild. Otherwise, skip this step.

4. **Deploy Stage**:
   - For the **Deploy Provider**, select **Amazon S3**.
   - Specify the bucket name where the files will be deployed.
   - Choose the destination for the build artifacts (e.g., the root of the S3 bucket).

5. **Review and Create**:
   - Review your pipeline settings and click **Create Pipeline**.

### 4. Automate Deployment

Once the pipeline is set up, every push to your GitHub repository will automatically trigger a new deployment to the S3 bucket.

### 5. Access Your Hosted Site

After deployment, your site will be accessible via the S3 bucket's website URL:

```
http://your-bucket-name.s3-website-your-region.amazonaws.com
```

