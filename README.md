# Terraform Unit Tests

GitHub action that runs Terraform unit tests.

## Inputs

| Name               | Required     | Description                                                                                                          |
| ------------------ | ------------ | -------------------------------------------------------------------------------------------------------------------- |
| `backend-config`    | **Optional** | The backend config file to use when running `terraform init`.                                                                             |
| `format`          | **Optional** | Whether or not to run `terraform fmt -recursive`. Default is true.              |
| `personal-access-token`      | **Optional** | The GitHub personal access token to use when running `terraform init`. Specify if any modules are stored in private repositories.                                                 |
| `tflint`          | **Optional** | Whether or not to run `tflint --recursive`. Default is true.                  |
| `tfsec` | **Optional** | Whether or not to run `tfsec`. Default is true. |
| `validate` | **Optional** | Whether or not to run `terraform validate`. Default is true. |
| `working-directory` | **Optional** | The working directory to run tests in. |

## Example Usage

### Basic

```yaml
- name: Configure AWS Credentials
  uses: aws-actions/configure-aws-credentials@v4
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: us-east-1

- name: Setup Terraform
  uses: hashicorp/setup-terraform@v3
  with:
    terraform_version: "1.1.7"

- name: Deploy CloudFront Function
  uses: dhollerbach/actions.terraform-unit-tests@v1
```

### Advanced

```yaml
- name: Configure AWS Credentials
  uses: aws-actions/configure-aws-credentials@v4
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: us-east-1

- name: Setup Terraform
  uses: hashicorp/setup-terraform@v3
  with:
    terraform_version: "1.1.7"

- name: Deploy CloudFront Function
  uses: dhollerbach/actions.terraform-unit-tests@v1
  with:
    backend-config: backend.conf
    personal-access-token: ${{ secrets.PAT }}
    tfsec: false
    working-directory: ./infra/
```
