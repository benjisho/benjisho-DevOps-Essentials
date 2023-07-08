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

## Step 1: Install Terraform

1. Open a terminal.

2. Download the latest version of Terraform from the official website (https://www.terraform.io/downloads.html).

3. Extract the downloaded archive to obtain the Terraform binary.

4. Move the Terraform binary to a directory in your system's `PATH` to make it executable.

5. Verify the Terraform installation by running the following command:
   ```
   terraform version
   ```
7. You should see the Terraform version displayed in the output.

## Step 2: Define Infrastructure with Terraform
1. Create a new directory for your Terraform project.

2. Inside the project directory, create the following files and directories for organizing your Terraform configuration:

```
├── main.tf
├── variables.tf
├── outputs.tf
├── modules/
│   ├── module1/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── module2/
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

4. In the `variables.tf` file, define input variables that allow customization of your Terraform configuration.

5. In the `outputs.tf` file, define output values that provide information about the created resources.

6. Inside the modules directory, create separate directories for each module you want to define. Each module should have its own `main.tf`, `variables.tf`, and `outputs.tf` files.

7. Inside the environments directory, create separate directories for each environment, such as prod and staging. Each environment should have its own `main.tf`, `variables.tf`, and `outputs.tf` files.

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
