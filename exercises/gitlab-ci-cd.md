# Exercise 2: Implementing CD with GitLab CI/CD

In this exercise, you will learn how to implement Continuous Delivery (CD) using GitLab CI/CD. By the end of this exercise, you will have a basic CD pipeline configured in GitLab.

## Table of Contents

- [Step 1: Install GitLab on your Vultr environment](#step-1-install-gitlab-on-your-vultr-environment)
- [Step 2: Create a sample project and configure CI/CD pipeline](#step-2-create-a-sample-project-and-configure-cicd-pipeline)
- [Step 3: Verify the CI/CD pipeline](#step-3-verify-the-cicd-pipeline)

## Prerequisites

Before starting this exercise, ensure that you have the following:

- A Vultr environment set up to install GitLab.
## Step 1: Install GitLab on your Vultr environment

1. Follow the official GitLab installation documentation:

   - For Ubuntu: [GitLab Installation Documentation for Ubuntu](https://docs.gitlab.com/)

2. Install GitLab for Ubuntu according to the provided instructions in the documentation.

3. Alternatively, you can use the [One-Click GitLab](https://www.vultr.com/docs/one-click-gitlab/) option provided by Vultr to quickly set up a GitLab environment.

4. Additionally, you may create an account on https://gitlab.com/ and set up a project there.

## Step 2: Create a sample project and configure CI/CD pipeline

1. Once GitLab is installed, access the GitLab web interface.

2. Create a new project or navigate to an existing project.

3. In the project settings, navigate to the "CI/CD" section.

4. Configure your CI/CD pipeline by defining stages and jobs using the `.gitlab-ci.yml` file.

   - Define stages for building, testing, packaging, and deploying the application.
   - Use appropriate GitLab CI/CD syntax to define jobs and their respective commands or scripts.

5. Commit and push the `.gitlab-ci.yml` file to trigger the pipeline execution.

## Step 3: Verify the CI/CD pipeline

1. Monitor the pipeline execution in the GitLab web interface.

2. Check the build logs, test results, and deployment status.

3. Verify that the application is successfully deployed to the target environment.

Congratulations! You have set up a basic CD pipeline using GitLab CI/CD.

