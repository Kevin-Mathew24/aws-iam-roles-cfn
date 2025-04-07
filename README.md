# AWS IAM Roles CloudFormation

This repository contains CloudFormation templates for creating IAM roles and policies for Lambda and S3 services following AWS best practices. It also includes GitHub Actions workflows to automatically deploy the CloudFormation stacks to AWS.

## Architecture

The CloudFormation template creates the following resources:

- **Lambda Execution Role**: A role with the necessary permissions for Lambda functions to execute
- **Lambda Basic Execution Policy**: Managed policy for CloudWatch Logs access
- **Lambda S3 Access Policy**: Managed policy for accessing S3 buckets with least privilege principles
- **S3 Bucket Role**: A role for S3 bucket operations
- **S3 Bucket Access Policy**: Managed policy for S3 bucket operations

## IAM Best Practices Implemented

1. **Least Privilege Access**: Only the minimum necessary permissions are granted
2. **Resource-Level Permissions**: Policies specify exact resources where possible
3. **Condition-Based Access**: Uses conditions to further restrict access where appropriate
4. **Environment-Based Scoping**: Resources are scoped to specific environments (dev, test, stage, prod)
5. **Clear Tagging Strategy**: All resources have appropriate tags
6. **Named Resources**: Resources are named consistently for better tracking
7. **Exported Outputs**: Stack outputs are exported for cross-stack references

## Repository Structure

```
├── .github/
│   └── workflows/
│       └── deploy-cfn.yml      # GitHub Actions workflow for deployment
├── templates/
│   └── iam-roles.yml          # CloudFormation template for IAM roles and policies
└── README.md                   # This file
```

## Deployment

### Automatic Deployment

The CloudFormation stack is automatically deployed when changes are pushed to the `main` branch that affect files in the `templates/` directory.

### Manual Deployment

You can also manually trigger a deployment from the GitHub Actions tab by selecting the "Deploy CloudFormation Stack" workflow and clicking "Run workflow".

## Required GitHub Secrets

To use this repository, you need to set up the following GitHub secrets:

- `AWS_ACCESS_KEY_ID`: Your AWS access key ID
- `AWS_SECRET_ACCESS_KEY`: Your AWS secret access key
- `AWS_REGION`: The AWS region to deploy to (e.g., `us-east-1`)

### Setting up GitHub Secrets

1. Go to your repository on GitHub
2. Click on "Settings" > "Secrets and variables" > "Actions"
3. Click on "New repository secret"
4. Add each of the required secrets

## Security Considerations

- The AWS access key used should have the minimum necessary permissions to deploy CloudFormation stacks and IAM resources
- Consider using OpenID Connect (OIDC) for more secure GitHub Actions authentication to AWS
- Regularly rotate your AWS credentials
- Review generated IAM policies and roles for any potential security issues

## Customization

You can customize the CloudFormation template to add additional permissions or roles as needed for your specific use case.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
