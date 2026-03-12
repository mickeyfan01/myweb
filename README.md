# My Personal Website - Infrastructure Engineering Challenge

This repository contains a solution for the Infrastructure Engineering challenge. The goal was to demonstrate my approach to creating a simple static website hosted on AWS using best practices and automated deployment.


## Project Overview

This project hosts a static website displaying a simple message including my name:

This is Mickey Fan’s website

can test run using the [url](https://dd054gwpxvlkp.cloudfront.net/)

The website is deployed on AWS S3 and served via CloudFront with automated deployment through GitHub Actions.

## Architecture & Infrastructure

### AWS S3 
- Stores the static website files
- bucket configured for private access
- public access is handled through CloudFront’s Origin Access Control (OAC).

### AWS CloudFront 
- Acts as a global CDN to serve the website with low latency
- Configured to redirect all HTTP traffic to HTTPS.
- Uses cache invalidation automatically after each deployment.

### GitHub Actions CI/CD Workflow steps:
- Checks out the repository.
- Assumes an AWS IAM role using OIDC for secure access.
- Creates or updates the S3 bucket.
- Uploads website files (excluding .git, .github, and README.md).
- Creates or updates the CloudFront distribution and OAC.
- Updates the S3 bucket policy to allow CloudFront access.
- Invalidates the CloudFront cache to serve updated content.
- The final deployment URL is printed for verification.

## Steps to Replicate
- Fork or clone this repository.
- Configure a GitHub Actions OIDC role in AWS with S3 and CloudFront permissions.
- Update BUCKET_NAME, AWS_REGION, and IAM role ARN in the workflow.
- Push changes to main branch or trigger the workflow manually.
- GitHub Actions will automatically deploy the site to S3 and CloudFront.
- Access the website using the CloudFront URL displayed at the end of the workflow.


## What I Would Do With More Time
### Custom Domain & SSL
- Use Route 53 to map a custom domain to CloudFront.
- Provision a custom SSL certificate via AWS Certificate Manager.

### Enhanced CI/CD
- Add automated testing (e.g., link checks, HTML validation) before deployment.
- Implement staging and production environments.

### Monitoring & Security
- Enable CloudFront logs and CloudWatch metrics for monitoring.
- Add WAF rules for protection against common web attacks.

### Scalability & Resilience
- Enable S3 cross-region replication for disaster recovery.
- Use versioning and lifecycle policies for rollback and backup.

## Alternative Approaches
### AWS Amplify
- Provides an all-in-one hosting solution with CI/CD.
- I didn’t use it here to show manual control and understanding of the underlying infrastructure.

### GCP Hosting
- Google Cloud Storage + Cloud CDN would offer similar functionality.
- AWS was chosen due to familiarity

## Production-Grade Considerations

### Infrastructure as Code (IaC)
 - Use Terraform to provision S3, CloudFront, OAC resources automatically.

### Multi-Environment CI/CD
 - Separate staging and production deployments
 - Include automated validation tests before promotion.

### Security & Compliance 
 - Enforce least-privilege IAM policies
 - Enable encryption at rest and in transit (S3 and CloudFront)
 - Regularly audit access logs.

### Collaboration 
 - Document release processes
 - rollback procedures
 - monitoring dashboards.

## Final Notes

This solution demonstrates:
- Laziness: Fully automated deployment via GitHub Actions, reducing manual effort.
- Impatience: CloudFront ensures fast, global content delivery.
- Hubris: Thoughtful consideration for production-readiness, security, and scalability.

The website is simple yet demonstrates best practices in infrastructure engineering, CI/CD automation, and cloud architecture.
