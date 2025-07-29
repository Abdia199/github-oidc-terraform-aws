 Problems I Encountered + Troubleshooting Tips

❌ Error: Not authorized to perform sts:AssumeRoleWithWebIdentity
Cause: The AWS credentials action version was outdated.
Fix:

Update the action from aws-actions/configure-aws-credentials@v1 to @v4.

Double-check the IAM Role ARN in GitHub Secrets (AWS_Role) and update it to match exactly.

Ensure the IAM Role trust policy includes the correct GitHub repo, e.g.:

json
Copy
Edit
"token.actions.githubusercontent.com:sub": "repo:Abdia199/github-oidc-terraform-aws:*"
❌ Too many command line arguments. Did you mean to use -chdir?
Cause: Syntax error due to multiline or newline issues in the terraform init command.
Fix: Write the entire terraform init command on a single line or use proper YAML multiline syntax:

yaml
Copy
Edit
run: terraform init -backend-config="bucket=${AWS_BUCKET_NAME}" -backend-config="key=${AWS_BUCKET_KEY_NAME}" -backend-config="region=${AWS_REGION}"
❌ AWS Region error
Cause: Incorrect or missing AWS_REGION secret in GitHub.
Fix: Ensure the secret AWS_REGION is set correctly and matches the value used in the workflow.

❌ Backend config mismatch
Cause: Terraform backend config keys do not match GitHub Secrets.
Fix: Confirm the names match exactly in both your workflow YAML and Terraform backend block. For example, the secret name must be AWS_BUCKET_NAME and referenced exactly:

yaml
Copy
Edit
-backend-config="bucket=${{ secrets.AWS_BUCKET_NAME }}"
