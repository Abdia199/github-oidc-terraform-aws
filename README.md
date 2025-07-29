
This project automates the deployment of AWS infrastructure using Terraform, authenticated via GitHub Actions and OpenID Connect (OIDC). It uses GitHub Actions to run Terraform commands such as init, plan, and apply whenever changes are pushed to the repository.

By leveraging OIDC, the workflow assumes an IAM role without hardcoding AWS credentials. Terraform state is stored securely in an S3 bucket, enabling collaboration and tracking. This setup ensures infrastructure changes are repeatable, secure, and fully automated — streamlining the DevOps workflow and eliminating manual provisioning through the AWS Console.

## 🧭 Overview

The GitHub Actions workflow in `.github/workflows/main.yml` performs the following:

- Checks out the code
- Configures AWS credentials using the GitHub OIDC token and assumes an IAM role
- Sets up Terraform CLI (version 1.2.5)
- Validates Terraform formatting (`terraform fmt`)
- Runs `terraform init` with S3 backend configuration
- Validates Terraform configuration syntax (`terraform validate`)
- Runs `terraform plan` on pull requests and posts the output as comments
- Applies Terraform changes on pushes to the `main` branch

---

## 📌 Prerequisites

1. **AWS IAM Role**: Set up an IAM Role with a trust policy allowing GitHub’s OIDC provider to assume the role. The trust policy should specify your GitHub repository and branch references.

2. **GitHub Secrets**: Add the following secrets to your repository settings:
   - `AWS_ROLE` — The ARN of the IAM role to assume
   - `AWS_REGION` — The AWS region (e.g., `us-east-1`)
   - `AWS_BUCKET_NAME` — S3 bucket name for Terraform state backend
   - `AWS_BUCKET_KEY_NAME` — The key/path in the S3 bucket for Terraform state

---

## 🖼️ Architecture / Workflow Diagram

<!-- Paste your architecture or GitHub Actions workflow diagram here -->
<img width="851" height="372" alt="image" src="https://github.com/user-attachments/assets/75cd666d-642d-4cd7-8684-141cbcd4f839" />





## 🚀 Usage

- Push changes to a feature branch and open a pull request against `main`.
- The workflow will run `terraform plan` and post the plan as a comment on the PR.
- Once reviewed, merge the PR to `main` to automatically trigger `terraform apply`.



## 🛠️ Notes

- The workflow uses `aws-actions/configure-aws-credentials@v4` for AWS authentication with OIDC.
- Ensure the IAM role trust policy includes the correct GitHub OIDC provider URL and matches your repository and branch patterns.
- Terraform state is managed remotely in an S3 bucket as configured in `terraform init`.



## 📄 License

This project is licensed under the MIT License.



*Created by Abdia199*
