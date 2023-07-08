# Exercise 2: Implementing CD with GitLab CI/CD

In this exercise, you will learn how to implement Continuous Delivery (CD) using GitLab CI/CD. By the end of this exercise, you will have a basic CD pipeline configured in GitLab.

## Table of Contents

- [Step 1: Install GitLab on your Vultr environment](#step-1-install-gitlab-on-your-vultr-environment)
- [Step 2: Create a sample project and configure CI/CD pipeline](#step-2-create-a-sample-project-and-configure-cicd-pipeline)
- [Step 3: Verify the CI/CD pipeline](#step-3-verify-the-cicd-pipeline)

## Prerequisites

Before starting this exercise, ensure that you have the following:

- A Vultr environment set up to install GitLab.
## Step 1: Setup/Install GitLab on your Vultr environment

1. You may create an account on https://gitlab.com/ and set up a project there.
2. Alternatively, you can use the [One-Click GitLab](https://www.vultr.com/docs/one-click-gitlab/) option provided by Vultr to quickly set up a GitLab environment.
3. Additionally, if you want to go through the manual process, you may follow the official GitLab installation documentation:
   - For Ubuntu: [GitLab Installation Documentation for Ubuntu](https://docs.gitlab.com/)
     Install GitLab for Ubuntu according to the provided instructions in the documentation.
## Step 2: Create a sample project and configure CI/CD pipeline

1. Once GitLab is installed, access the GitLab web interface by opening your web browser and navigating to the GitLab URL. If you installed GitLab locally, the URL might be http://localhost or http://localhost:3000 by default. If you are using GitLab's hosted service on gitlab.com, access your project by logging into your gitlab.com account.

2. Create a new project or navigate to an existing project where you want to configure the CI/CD pipeline. If you're creating a new project, provide a name and optionally a description for your project. Click on the "Create project" button to create the project.

3. In the project settings, navigate to the "Set Up CI/CD" section. This section allows you to configure and manage the CI/CD pipeline for your project.

## Step 3: Configuring the CI/CD pipeline
1. To configure your CI/CD pipeline, you need to define stages and jobs using the .gitlab-ci.yml file. This file should be located in the root directory of your GitLab project.

2. The .gitlab-ci.yml file follows a YAML syntax and allows you to define the stages of your pipeline and the jobs that run within each stage. Here's an example of a basic .gitlab-ci.yml file:
   ```
   stages:
     - build
     - test
     - deploy

   build_job:
     stage: build
     script:
       - echo "Building the application..."

   test_job:
     stage: test
     script:
       - echo "Running tests..."

   deploy_job:
     stage: deploy
     script:
       - echo "Deploying the application..."
   ```
   - In this example, we have three stages defined: build, test, and deploy. Each stage contains a single job with its own script. The script defines the commands or scripts that are executed as part of that job.
   - Feel free to customize the stages and jobs according to your project's requirements. You can add more stages, define dependencies between jobs, and include more complex commands or scripts.

3. Once you have defined the .gitlab-ci.yml file, commit and push it to your GitLab repository. This action will trigger the pipeline execution based on the configuration defined in the file.

## Step 3: Monitoring the CI/CD pipeline
1. After pushing the .gitlab-ci.yml file, you can monitor the pipeline execution in the GitLab web interface. Go to your project's page and navigate to the "CI/CD" section. Here, you will see the pipeline status, including the stages and jobs that are currently running or have completed.

2. Clicking on the pipeline will provide more details, such as the build logs, test results, and deployment status for each job in the pipeline.

## Step 4: Verifying the CI/CD pipeline
1. To verify that the CI/CD pipeline is working as expected, check the logs and status of each job. The build job should successfully build your application, the test job should run your tests and report the results, and the deploy job should deploy your application to the target environment.

2. If any job fails or encounters errors, investigate the logs and error messages to identify the cause and make necessary adjustments to your pipeline configuration or application code.

Congratulations! You have successfully created and configured a basic CI/CD pipeline using GitLab CI/CD.
