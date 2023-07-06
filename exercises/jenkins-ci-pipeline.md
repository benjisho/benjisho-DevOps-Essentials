# Exercise 1: Setting up a CI Pipeline with Jenkins

In this exercise, you will learn how to set up a CI pipeline using Jenkins. By the end of this exercise, you will have a basic CI pipeline configured in Jenkins.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Install Jenkins on your Ubuntu machine](#step-1-install-jenkins-on-your-ubuntu-machine)
- [Step 2: Access Jenkins and set up the initial configuration](#step-2-access-jenkins-and-set-up-the-initial-configuration)
- [Step 3: Set up a basic CI pipeline](#step-3-set-up-a-basic-ci-pipeline)
- [Step 4: Trigger the CI pipeline](#step-4-trigger-the-ci-pipeline)

## Prerequisites

- Ubuntu machine with Java installed (see Step 1)
- Access to the Jenkins web interface

## Step 1: Install Jenkins on your Ubuntu machine

1. Open a terminal.

2. Run the following commands to install Java, which is a prerequisite for Jenkins:
   ```
   bash
   sudo apt update
   sudo apt install default-jdk
   ```
3. Add the Jenkins repository key to your system:
   ```
   wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
   ```
4. Add the Jenkins repository to your system:
   ```
   sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
   ```
5. Update your package list:
   ```
   sudo apt update
   ```
6. Install Jenkins:
   ```
   sudo apt install jenkins
   ```
7. Start Jenkins as a service:
   ```
   sudo systemctl start jenkins
   ```
8. Enable Jenkins to start on boot:
   ```
   sudo systemctl enable jenkins
   ```
## Step 2: Access Jenkins and set up the initial configuration
 1. Open a web browser and navigate to http://localhost:8080 (assuming you're accessing it on your local machine).
 2. Retrieve the Jenkins initial admin password:
    ```
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
 3. Copy the password from the terminal.
 4. Paste the password into the Jenkins web page.
 5. Click on "Install suggested plugins" to install the recommended plugins.
 6. Create an admin user and provide the necessary details.
 7. Click on "Save and Finish" and then "Start using Jenkins."

## Step 3: Set up a basic CI pipeline
 1. On the Jenkins homepage, click on "New Item" to create a new job.
 2. Enter a name for your job (e.g., "My CI Pipeline") and select "Freestyle project."
 3. In the configuration page, under the "General" section, check the "GitHub project" checkbox and enter the URL of your sample project repository.
 4. Under the "Build" section, click on "Add build step" and select the appropriate build step for your project (e.g., "Execute shell" for a simple script).
 5. Enter the necessary build commands or script in the text area.
 6. Click on "Save" to save the configuration.

## Step 4: Trigger the CI pipeline
 1. On the Jenkins homepage, locate your job and click on "Build Now" to manually trigger the pipeline.
 2. Jenkins will start the build process, executing the defined build steps and displaying the console output.
 3. Monitor the build status and console output for any errors or issues.

Congratulations! You have set up a basic CI pipeline using Jenkins.
