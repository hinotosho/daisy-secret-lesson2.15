# daisy-secret-lesson2.15
CE9 Lesson 2.15 Homework

1. What is Needed to Authorize Your EC2 to Retrieve Secrets from AWS Secrets Manager?

To authorize an EC2 instance to access AWS Secrets Manager, follow these key steps:

Step 1: Create an IAM Policy & IAM role

Create an IAM Policy, create an IAM role and attach the policy to the IAM role.

Use an AWS-managed or custom policy granting secretsmanager:GetSecretValue.

Step 2: Attach the IAM Role to the EC2 Instance

Attach the IAM Role with the IAM policy to the EC2 instance to allow Secrets Manager access. Ensure the EC2 instance is using an IAM Instance Profile with the correct permissions.

Check under EC2 → Security → IAM Role to verify.

Step 3: Limit Access to Specific Secrets

Use resource-specific permissions so the EC2 instance only accesses necessary secrets instead of full access.

2. Derive the IAM Policy (JSON Format)
   
Below is a secure IAM policy that allows EC2 to retrieve a specific secret (prod/cart-service/credentials) from AWS Secrets Manager:

json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "secretsmanager:GetSecretValue",
      "Resource": "arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials-*"
    }
  ]
}
Explanation of the IAM Policy
- Allows only secretsmanager:GetSecretValue (not full access).
- Restricts access to a specific secret ARN (prod/cart-service/credentials).
- Uses wildcards (-*) for secrets that may have versions.

3. Deriving the Correct ARN for my Secret
   
AWS Secrets Manager secrets follow this ARN format:

arn:aws:secretsmanager:<region>:<account-id>:secret:<secret-name>
For the secret prod/cart-service/credentials, the derived ARN would be:

arn:aws:secretsmanager:us-east-1:123456789012:secret:prod/cart-service/credentials

Verifying the ARN
✔ ap-southeast-1 → Singapore AWS Region. ✔ 123456789012 → Replace with my AWS Account ID. ✔ prod/cart-service/credentials → The secret name in AWS Secrets Manager.
