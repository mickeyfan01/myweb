# My Personal Website - Infrastructure Engineering Challenge

This repository contains my solution to the Infrastructure Engineering challenge. The objective was to demonstrate a clean, secure and automated approach for hosting a simple static website on AWS using cloud practise.


## Project Overview

This project deploys a lightweight static website that deploys a simple message: 

``` This is Mickey Fan’s website ```

you can test the running using this [url](https://dd054gwpxvlkp.cloudfront.net/)

The website is hosted on AWS S3 and delivered globally through Amazon CloudFront with fully automated deployment powered by GitHub Actions.

## Architecture & Infrastructure

### AWS S3 
- Stores the static website content
- Bucket configured for private access
- CloudFront access is controlled using Origin Access Control (OAC)

### AWS CloudFront 
- Servces the website via a global CDN for low latency
- Configured to redirect all HTTP traffic to HTTPS
- invalidation cache after each deployment

### GitHub Actions CI/CD Pipeline 
The workflow perform the following steps:
1. Checks out the repository
2. Assumes an AWS IAM role using OIDC for secure authenication
3. Creates or updates the S3 bucket
4. Uploads website files (excluding .git, .github, and README.md)
5. Creates or updates the CloudFront distribution and OAC
6. Updates the S3 bucket policy to allow CloudFront access
7. Invalidates the CloudFront cache
8. Print the final deployment URL for verification

## Steps to Replicate
1. Fork or clone this repository
2. Configure a GitHub Actions OIDC role in AWS with S3 and CloudFront permissions.
3. Update BUCKET_NAME, AWS_REGION, and IAM role ARN in the workflow
4. Push changes to main branch or trigger the workflow manually
5. GitHub Actions will automatically deploy the site to S3 and CloudFront
6. Access the website using the CloudFront URL displayed at the end of the workflow


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
A fully managed hosting CI/CD solution and I intetntionaly avoid Amplify to demonstrate explicit control of the underlying AWS infrastructure

### GCP Hosting
Hosting could be achieved with Google Cloud Storage + Cloud CDN and AWS was chosen due to familiarity

## Production-Grade Considerations

### Infrastructure as Code (IaC)
 - Use Terraform to provision S3, CloudFront, OAC resources automatically.

### Multi-Environment CI/CD
 - Separate staging and production deployments
 - Include automated validation tests before promoting release

### Security & Compliance 
 - Enforce strict least-privilege IAM policies
 - Enable encryption at rest and in transit
 - Regularly audit access logs

### Collaboration 
 - Document release processes
 - rollback procedures
 - monitoring dashboards.

## Final Notes

This solution demonstrates:
- Laziness: Fully automated deployment via GitHub Actions, reducing manual effort.
- Impatience: CloudFront ensures fast, global content delivery.
- Hubris: Thoughtful consideration for production-readiness, security, and scalability.

The website is simple yet demonstrates best practices in infrastructure engineering, CI/CD automation and cloud architecture.
