# Exercise: Infrastructure Provisioning with Terraform

In this exercise, you will learn how to use Terraform to provision infrastructure resources. Terraform allows you to define and manage your infrastructure as code, making it easier to create and manage your infrastructure across various cloud providers. By the end of this exercise, you will have hands-on experience with provisioning infrastructure using Terraform.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Install Terraform](#step-1-install-terraform)
- [Step 2: Define Infrastructure with Terraform](#step-2-define-infrastructure-with-terraform)
- [Step 3: Provision Infrastructure with Terraform](#step-3-provision-infrastructure-with-terraform)
- [Step 4: Manage Infrastructure with Terraform](#step-4-manage-infrastructure-with-terraform)

## Prerequisites

- Terraform installed on your Ubuntu machine
- Basic knowledge of infrastructure concepts and cloud providers (e.g., AWS, Azure, GCP)
- AWS account (https://aws.amazon.com/)
- Vultr account (https://www.vultr.com/)

## Step 1: Install Terraform

1. Open a terminal.

2. Run the following commands to add the HashiCorp GPG key and repository to your system:
   ```
   wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
   echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
   sudo apt update
   ```
3. Install Terraform using the package manager:
   ```
   sudo apt install terraform
   ```
4. Verify the Terraform installation by running the following command:
   ```
   terraform version
   ```
You should see the Terraform version displayed in the output.

## Step 2: Define Infrastructure with Terraform
1. Create a new directory for your Terraform project.

2. Inside the project directory, create the following files and directories for organizing your Terraform configuration:

    ```
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf
    ├── modules/
    │   ├── aws/
    │   │   ├── main.tf
    │   │   ├── variables.tf
    │   │   └── outputs.tf
    │ └── vultr/
    │ ├── main.tf
    │ ├── variables.tf
    │ └── outputs.tf
    │   └── module3/
    │       ├── main.tf
    │       ├── variables.tf
    │       └── outputs.tf
    ├── environments/
    │   ├── prod/
    │   │   ├── main.tf
    │   │   ├── variables.tf
    │   │   └── outputs.tf
    │   └── staging/
    │       ├── main.tf
    │       ├── variables.tf
    │       └── outputs.tf
    ├── terraform.tfvars
    └── README.md
    ```

3. In the `main.tf` file, define the main Terraform configuration. This file can include provider configuration, resource definitions, and data sources.

    **Example `main.tf`:**

    ```
    terraform {
      required_providers {
        aws = {
          source  = "hashicorp/aws"
          version = "3.48.0"
        }
        vultr = {
          source  = "vultr/vultr"
          version = "2.19.0"
        }
      }
    }

    provider "aws" {
      region = var.aws_region
    }

    provider "vultr" {
      api_key = var.vultr_api_key
    }

    resource "aws_instance" "example" {
      ami           = var.aws_ami
      instance_type = var.aws_instance_type
      tags = {
        Name = "Example Instance"
      }
    }

    resource "vultr_server" "example" {
      plan     = "vc2-1c-1gb"
      region   = var.vultr_region
      hostname = "example-vultr-server"
    }
    ```
  4. In the `variables.tf` file, define input variables that allow customization of your Terraform configuration.
   
      **Example `variables.tf`:**

        ```
        variable "aws_region" {
          description = "AWS region"
          type        = string
          default     = "us-west-2"
        }

        variable "vultr_region" {
          description = "Vultr region"
          type        = string
          default     = "ams"
        }

        variable "aws_ami" {
          description = "AMI ID for AWS"
          type        = string
          default     = "ami-0c94855ba95c71c99"
        }

        variable "aws_instance_type" {
          description = "EC2 instance type for AWS"
          type        = string
          default     = "t2.micro"
        }

        variable "vultr_plan" {
          description = "Vultr plan"
          type        = string
          default     = "vc2-2c-4gb"
        }

        variable "vultr_api_key" {
          description = "Vultr API key"
          type        = string
          sensitive   = true
        }
        ```

5. In the `outputs.tf` file, define output values that provide information about the created resources.

    **Example `outputs.tf`:**

    ```
    output "aws_instance_id" {
      description = "ID of the created AWS EC2 instance"
      value       = aws_instance.example.id
    }

    output "vultr_server_id" {
      description = "ID of the created Vultr server"
      value       = vultr_server.example.id
    }
    ```

6. Inside the modules directory, create separate directories for each module you want to define. Each module should have its own `main.tf`, `variables.tf`, and `outputs.tf` files.

    *AWS*

    **Example `modules/aws/main.tf`:**

    ```
    resource "aws_s3_bucket" "example" {
    bucket = var.bucket_name
    acl    = "private"
    }
    ```

    **Example `modules/aws/variables.tf`:**

    ```
    variable "bucket_name" {
    description = "Name of the S3 bucket"
    type        = string
    }
    ```

    **Example `modules/aws/outputs.tf`:**

    ```
    output "bucket_arn" {
    description = "ARN of the created S3 bucket"
    value       = aws_s3_bucket.example.arn
    }  
    ```

    *Vultr*

    **Example modules/vultr/main.tf:**

    ```
    resource "vultr_block_storage" "example" {
    label = var.vultr_block_storage_label
    size  = var.vultr_block_storage_size
    region = var.vultr_region
    }
    ```

    **Example modules/vultr/variables.tf:**

    ```
    variable "vultr_block_storage_label" {
      description = "Label for the Vultr block storage"
      type        = string
    }

    variable "vultr_block_storage_size" {
      description = "Size of the Vultr block storage in GB"
      type        = number
    }
    ```

    **Example modules/vultr/outputs.tf:**

    ```
    output "vultr_block_storage_id" {
      description = "ID of the created Vultr block storage"
      value       = vultr_block_storage.example.id
    }
    ```
7. Inside the environments directory, create separate directories for each environment, such as prod and staging. Each environment should have its own `main.tf`, `variables.tf`, and `outputs.tf` files.
    **Example `environments/prod/main.tf`:**

    ```
    module "aws_resources" {
      source = "../modules/aws"

      aws_bucket_name = var.prod_aws_bucket_name
    }

    module "vultr_resources" {
      source = "../modules/vultr"

      vultr_block_storage_label = var.prod_vultr_block_storage_label
      vultr_block_storage_size  = var.prod_vultr_block_storage_size
    }
    ```

    **Example `environments/prod/variables.tf`:**

    ```
    variable "prod_aws_bucket_name" {
      description = "Name of the production AWS S3 bucket"
      type        = string
    }

    variable "prod_vultr_block_storage_label" {
      description = "Label for the production Vultr block storage"
      type        = string
    }

    variable "prod_vultr_block_storage_size" {
      description = "Size of the production Vultr block storage in GB"
      type        = number
    }

    ```

    **Example `environments/prod/outputs.tf`:**

    ```
    output "prod_aws_bucket_arn" {
      description = "ARN of the created production AWS S3 bucket"
      value       = module.aws_resources.aws_bucket_arn
    }

    output "prod_vultr_block_storage_id" {
      description = "ID of the created production Vultr block storage"
      value       = module.vultr_resources.vultr_block_storage_id
    }

    ```

    **Example `environments/staging/main.tf`:**

    ```
    module "aws_resources" {
      source = "../modules/aws"

      aws_bucket_name = var.staging_aws_bucket_name
    }

    module "vultr_resources" {
      source = "../modules/vultr"

      vultr_block_storage_label = var.staging_vultr_block_storage_label
      vultr_block_storage_size  = var.staging_vultr_block_storage_size
    }
    ```

    **Example `environments/staging/variables.tf`:**

    ```
    variable "staging_aws_bucket_name" {
      description = "Name of the staging AWS S3 bucket"
      type        = string
    }

    variable "staging_vultr_block_storage_label" {
      description = "Label for the staging Vultr block storage"
      type        = string
    }

    variable "staging_vultr_block_storage_size" {
      description = "Size of the staging Vultr block storage in GB"
      type        = number
    }
    ```

    **Example `environments/staging/outputs.tf`:**
    
    ```
    output "staging_aws_bucket_arn" {
      description = "ARN of the created staging AWS S3 bucket"
      value       = module.aws_resources.aws_bucket_arn
    }

    output "staging_vultr_block_storage_id" {
      description = "ID of the created staging Vultr block storage"
      value       = module.vultr_resources.vultr_block_storage_id
    }
    ```
8. Use module blocks in your `main.tf` and environment-specific configuration files to reference and configure modules.

## Step 3: Provision Infrastructure with Terraform
1. Run the following command in your project directory to initialize Terraform and download the necessary provider plugins:
    ```
    terraform init
    ```
2. Validate the Terraform configuration by running:
    ```
    terraform validate
    ```
3. Preview the infrastructure changes that Terraform will make by running:
    ```
    terraform plan
    ```
4. To plan and apply module-specific changes, navigate to the module directory and run the Terraform commands with the -target flag. For example:
    ```
    terraform plan -target=module.module1
    terraform apply -target=module.module1
    ```
5. To plan and apply environment-specific changes, navigate to the environment directory and run the Terraform commands. For example:
    ```
    terraform plan
    terraform apply
    ```
6. If the plan looks as expected, apply the infrastructure changes by running:
    ```
    terraform apply
    ```
7. You may be prompted to confirm the changes before proceeding.

8. Terraform will provision the defined infrastructure resources based on the configuration.

9. Verify that the infrastructure has been provisioned correctly by checking the resources in your cloud provider's console or using other appropriate tools.

## Step 4: Manage Infrastructure with Terraform
1. As your infrastructure evolves, make changes to the Terraform configuration to reflect the desired state of your infrastructure.

2. Use the terraform plan command to preview the changes and ensure they align with your expectations.

3. Apply the changes using the terraform apply command. Terraform will update your infrastructure to match the new configuration.

4. Regularly maintain and update your Terraform project to reflect changes in your infrastructure requirements.

Congratulations! You have successfully provisioned infrastructure using Terraform. This exercise provides a foundation for managing and scaling your infrastructure in a declarative and efficient manner.
