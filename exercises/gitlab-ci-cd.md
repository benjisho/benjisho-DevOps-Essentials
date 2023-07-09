# Exercise 2: Implementing CD with GitLab CI/CD

In this exercise, you will learn how to implement Continuous Delivery (CD) using GitLab CI/CD. By the end of this exercise, you will have a basic CD pipeline configured in GitLab.

## Table of Contents

- [Step 1: Install GitLab on your Vultr environment](#step-1-setupinstall-gitlab-on-your-vultr-environment)
- [Step 2: Create a sample project and configure CI/CD pipeline](#step-2-create-a-sample-project-and-configure-cicd-pipeline)
- [Step 3: Configuring the CI/CD pipeline](#step-3-configuring-the-cicd-pipeline)
  - [Step 3 Details](#step-3-details)
- [Step 4: Monitoring the CI/CD pipeline](#step-4-monitoring-the-cicd-pipeline)
- [Step 5: Verifying the CI/CD pipeline](#step-5-verifying-the-cicd-pipeline)
- [_Bonus Step: Advanced Configuration of CI/CD pipeline_](#bonus-step-advanced-configuration-of-cicd-pipeline)
  - [_Bonus Step Details_](#bonus-step-details)

## Prerequisites

Before starting this exercise, ensure that you have the following:

- A Vultr account for setup/access/install GitLab environment.
- Basic knowledge of Linux command-line interface (CLI).
  
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

## Step 3: Basic Configuration of CI/CD pipeline
1. To configure your CI/CD pipeline, you need to define stages and jobs using the .gitlab-ci.yml file.
   - This file should be located in the root directory of your GitLab project.

2. The .gitlab-ci.yml file follows a YAML syntax and allows you to define the stages of your pipeline and the jobs that run within each stage.
   - Here's an example of a basic .gitlab-ci.yml file:
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

   - In this example, we have three stages defined:
     - build
     - test
     - deploy
   - Each stage contains a single job with its own script.
   - The script defines the commands or scripts that are executed as part of that job.
   - Feel free to customize the stages and jobs according to your project's requirements.
     - You can add more stages, define dependencies between jobs, and include more complex commands or scripts.

3. Once you have defined the .gitlab-ci.yml file, commit and push it to your GitLab repository.
4. This action will trigger the pipeline execution based on the configuration defined in the file.

### Step 3 Details
- The `.gitlab-ci.yml` file is used to define the stages and jobs for your CI/CD pipeline.
- The `build_job` is defined in the build stage and runs the script to build the application.
- The `test_job` is defined in the test stage and runs the script to execute tests.
- The `deploy_job` is defined in the deploy stage and runs the script to deploy the application.

## Step 4: Monitoring the CI/CD pipeline
1. After pushing the .gitlab-ci.yml file, you can monitor the pipeline execution in the GitLab web interface. Go to your project's page and navigate to the "CI/CD" section. Here, you will see the pipeline status, including the stages and jobs that are currently running or have completed.

2. Clicking on the pipeline will provide more details, such as the build logs, test results, and deployment status for each job in the pipeline.

## Step 5: Verifying the CI/CD pipeline
1. To verify that the CI/CD pipeline is working as expected, check the logs and status of each job. The build job should successfully build your application, the test job should run your tests and report the results, and the deploy job should deploy your application to the target environment.

2. If any job fails or encounters errors, investigate the logs and error messages to identify the cause and make necessary adjustments to your pipeline configuration or application code.

---

## Bonus Step: Advanced Configuration of CI/CD pipeline
1. To configure your CI/CD pipeline, you need to define stages and jobs using the .gitlab-ci.yml file.
2. This file should be located in the root directory of your GitLab project.
3. Create a Dockerfile in the root directory of your project with the following content:
    ```
    FROM ubuntu:latest

    # Set environment variables
    ENV DEBIAN_FRONTEND noninteractive

    # Update the package lists
    RUN apt-get update -y

    # Install necessary packages
    RUN apt-get install -y \
        build-essential \
        curl \
        git \
        vim

    # Set the working directory
    WORKDIR /app

    # Copy the necessary files to the working directory
    COPY . /app

    # Set the entry point or default command
    CMD ["/bin/bash"]
    ```
4. In your .gitlab-ci.yml file, add the following stages and jobs:
    ```
    stages:
    - build
    - test
    - deploy

    build_job:
    stage: build
    image: docker:latest
    services:
        - docker:dind
    script:
        - docker build -t my-ubuntu-image .
        - docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD
        - docker push $DOCKER_USERNAME/my-ubuntu-image

    test_job:
      stage: test
      script:
        - echo "Running integration tests..."
        - docker run --rm my-ubuntu-image pytest
        - echo "Checking installed packages..."
        - docker run --rm my-ubuntu-image bash -c "dpkg -s build-essential curl git vim"

    deploy_job:
      stage: deploy
      script:
        - echo "Deploying the application..."
        - docker run -d --name my-ubuntu-app my-ubuntu-image
        - echo "Application deployed successfully!"
    rules:
      - if: $CI_JOB_NAME == "test_job"
        when: on_success
      - if: $CI_JOB_NAME == "deploy_job"
        when: on_success
        allow_failure: true
    ```
     > **Note: Make sure to set the `$DOCKER_USERNAME` and `$DOCKER_PASSWORD` environment variables in your GitLab CI/CD settings or CI/CD variables to authenticate and push the Docker image to your Docker Hub repository.**

5. This is a bit more advanced configuration.
   - It demonstrates how to:
     - build a Docker image
     - authenticate with Docker Hub
     - and push the image to a repository as part of the CI/CD pipeline.
7. In this example, we have added a build stage with a job that builds the Docker image using the Dockerfile we created. The image is tagged as `my-ubuntu-image`.
8. The `test_job` stage is included for running integration tests and checking the installed packages in the Docker image.
9. Finally, the `deploy_job` stage is included for deploying the application and run the container in the background.
10. Once you have defined the .gitlab-ci.yml file and the Dockerfile, commit and push them to your GitLab repository.
11. This action will trigger the pipeline execution based on the configuration defined in the file.

### Bonus Step Details
In this advanced configuration:
 - The `build_job` stage uses the `docker:latest` image and includes the `docker:dind` service, which allows running Docker commands inside the CI/CD environment.
 - The `script` section for the `build_job` includes additional steps to log in to Docker Hub (`docker login`) using the provided `$DOCKER_USERNAME` and `$DOCKER_PASSWORD` environment variables, and push the built image to the Docker Hub repository with the appropriate tag.
 - The `test_job` stage runs integration tests by executing `pytest` inside the `my-ubuntu-image` container.
   - It also checks the installed packages by running the `dpkg -s` command for `build-essential`, `curl`, `git`, and `vim` inside the container.
 - The `deploy_job` stage deploys the application by running the `docker run` command to start a container named `my-ubuntu-app` using the `my-ubuntu-image`.
 - The `rules` section specifies the execution rules for the jobs.
   - The `test_job` and `deploy_job` will only be executed on success of previous stages.
   - The `deploy_job` allows failure, meaning if it encounters an error, it will not fail the overall pipeline.

Congratulations! You now have an advanced CI/CD pipeline configuration that builds a Docker image, runs tests, and prepares for deployment.

---

Congratulations! You have successfully created and configured a basic CI/CD pipeline using GitLab CI/CD.

