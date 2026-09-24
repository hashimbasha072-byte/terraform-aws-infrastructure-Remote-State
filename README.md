# Terraform AWS Infrastructure

## 📌 Project Overview

This project demonstrates the use of **Terraform** to provision and manage AWS infrastructure using **Infrastructure as Code (IaC)**.

Instead of creating AWS resources manually through the AWS Management Console, Terraform configuration files are used to define the desired infrastructure and manage its lifecycle.

The project was completed as a hands-on Cloud and DevOps practice project.

---

## 🎯 Objective

The main objective of this project was to gain practical experience with:

* Infrastructure as Code
* Terraform configuration
* AWS resource provisioning
* Terraform variables
* Terraform outputs
* Terraform state management
* Infrastructure lifecycle management

## ☁️ Remote State Management

The project also demonstrates managing Terraform state remotely using an **Amazon S3 bucket**.

Instead of keeping the Terraform state file only on the local machine, the state is stored in an S3 bucket. This provides centralized state storage and allows the Terraform state to be managed separately from the local project files.

### S3 Remote Backend

Example backend configuration:

```hcl
terraform {
  backend "s3" {
    bucket         = "YOUR-TERRAFORM-STATE-BUCKET"
    key            = "terraform/state/terraform.tfstate"
    region         = "ap-south-1"
    encrypt        = true
    dynamodb_table = "terraform-state-lock"
  }
}
```

### Remote State Architecture

```text
                Terraform
                    |
                    v
            S3 Remote Backend
                    |
                    v
          terraform.tfstate
                    |
                    v
          DynamoDB State Lock
```

### Why Remote State?

Remote state provides:

* Centralized Terraform state storage
* State persistence outside the local machine
* Encryption of the state object
* State locking to help prevent concurrent Terraform operations
* Better collaboration and infrastructure management

### State Locking with DynamoDB

A DynamoDB table was configured for Terraform state locking.

The purpose of state locking is to prevent multiple Terraform operations from modifying the same state simultaneously.

Example:

```text
Terraform User 1
       |
       v
  State Lock
       |
       X
Terraform User 2
```

When the first Terraform operation releases the lock, another operation can proceed.

### Backend Initialization

After configuring the S3 backend, Terraform was initialized using:

```bash
terraform init
```

Terraform then configured the remote backend and used the S3 location for storing the state.

### Security Considerations

The following were kept out of GitHub:

```text
terraform.tfstate
terraform.tfstate.backup
AWS access keys
AWS secret keys
Terraform credentials
```

The `.gitignore` file was configured to prevent sensitive Terraform state and credentials from being committed accidentally.


---

## 🛠️ Technologies Used

```text
Terraform
AWS
Amazon EC2
Amazon VPC
Linux
Git
GitHub
```

---

## 📁 Project Structure

```text
terraform-aws-infrastructure/
│
├── main.tf
├── variables.tf
├── terraform.tfvars
├── outputs.tf
├── .gitignore
└── README.md
```

---

## ⚙️ Terraform Configuration

### `main.tf`

The main Terraform configuration contains the AWS provider and infrastructure resource definitions.

Terraform uses these configuration files to determine which AWS resources need to be created or managed.

---

### `variables.tf`

Variables are defined separately to make the Terraform configuration reusable and easier to maintain.

Example:

```hcl
variable "region" {
  description = "AWS region"
  type        = string
}
```

---

### `terraform.tfvars`

The variable values are provided through `terraform.tfvars`.

Example:

```hcl
region = "ap-south-1"
```

Sensitive information should never be stored directly in the repository.

---

### `outputs.tf`

Terraform outputs are used to display useful information about the infrastructure after deployment.

Examples include:

* Resource IDs
* Public IP addresses
* VPC information
* Other resource attributes

---

## 🚀 Terraform Workflow

The project follows the standard Terraform workflow:

```text
Write Configuration
        |
        v
terraform init
        |
        v
terraform validate
        |
        v
terraform plan
        |
        v
terraform apply
        |
        v
AWS Infrastructure
        |
        v
terraform destroy
```

---

## 1. Initialize Terraform

Initialized the Terraform working directory:

```bash
terraform init
```

This downloads the required provider plugins and prepares the working directory.

---

## 2. Validate Configuration

Validated the Terraform configuration:

```bash
terraform validate
```

This checks whether the Terraform configuration is syntactically valid and internally consistent.

---

## 3. Format Configuration

Formatted the Terraform files using:

```bash
terraform fmt
```

This keeps the configuration consistently formatted.

---

## 4. Review Execution Plan

Generated an execution plan:

```bash
terraform plan
```

The plan shows what Terraform intends to create, modify, or destroy before making changes to AWS.

---

## 5. Provision Infrastructure

Applied the Terraform configuration:

```bash
terraform apply
```

After reviewing the proposed changes, the infrastructure was provisioned in AWS.

---

## 6. Verify Infrastructure

Verified the resources created by Terraform through the AWS Management Console and Terraform outputs.

The infrastructure created by Terraform was checked to ensure that the configuration was working as expected.

---

## 7. Destroy Infrastructure

After completing the practice, the infrastructure was removed using:

```bash
terraform destroy
```

This demonstrates the complete Terraform infrastructure lifecycle.

---

## 🔐 Terraform State

Terraform maintains a **state file** to keep track of the infrastructure resources it manages.

The local state file contains information about the resources managed by Terraform.

For security reasons, Terraform state files are excluded from Git using `.gitignore`.

Example:

```gitignore
.terraform/
*.tfstate
*.tfstate.*
```

AWS credentials and other sensitive information are also excluded from the repository.

---

## 🔄 Infrastructure as Code Workflow

```text
Terraform Configuration
        |
        v
Terraform Plan
        |
        v
Review Changes
        |
        v
Terraform Apply
        |
        v
AWS Infrastructure
        |
        v
Terraform Destroy
```

This approach makes infrastructure configuration more consistent, repeatable, and easier to manage.

---

## 📚 Key Concepts Learned

Through this project, I gained hands-on experience with:

* Infrastructure as Code
* Terraform providers
* Terraform resources
* Terraform variables
* Terraform outputs
* Terraform state
* Terraform initialization
* Terraform validation
* Terraform formatting
* Terraform planning
* Terraform apply
* Terraform destroy
* AWS infrastructure provisioning
* Infrastructure lifecycle management

---

## 🎯 Project Outcome

Successfully used Terraform to define, provision, verify, and destroy AWS infrastructure through Infrastructure as Code.

This project strengthened my practical understanding of **Terraform and AWS infrastructure automation**, which are important concepts in Cloud and DevOps engineering.

---

## 👨‍💻 Author

**A Mohammed Hashim**

BCA Graduate | AWS | Cloud Computing | DevOps | SRE

GitHub: https://github.com/hashimbasha072-byte

