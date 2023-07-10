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
- Internet connectivity on the machine that is going to download and install Jenkins and its dependencies.
- Basic knowledge of Ubuntu command-line interface (CLI) and package management (apt).
- Access to the Jenkins web interface (port http 8080)
- A sample project repository hosted on GitHub (or other version control platform) to configure the CI pipeline.

## Step 1: Install Jenkins on your Ubuntu machine

> Note: This installation guide is based on the official Jenkins documentation for Debian/Ubuntu. For more detailed information and alternative installation methods, refer to the [Jenkins documentation](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu).

1. Open a terminal.

2. Update the package lists and install OpenJDK 17 (Java Runtime Environment):
```
sudo apt update
sudo apt install openjdk-17-jre
```
3. Verify the Java installation by running the following command:
```
java -version
```
4. Import the Jenkins repository key:
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo gpg --dearmor --yes -o /usr/share/keyrings/jenkins-keyring.gpg
```
5. Add the Jenkins repository to your system:
```
echo 'deb [signed-by=/usr/share/keyrings/jenkins-keyring.gpg] https://pkg.jenkins.io/debian-stable binary/' | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```
6. Update your package list:
```
sudo apt update
```
7. Install Jenkins:
```
sudo apt install jenkins
```
8. Jenkins will be installed as a systemd service, and it will start automatically. You can check the status using the following command:
```
sudo systemctl status jenkins
```
9. By default, Jenkins listens on port 8080. Access the Jenkins web interface using your browser by visiting `http://<your-server-IP-or-domain>:8080`.

10. Follow the instructions displayed in the web interface to complete the initial Jenkins setup.

### Jenkins File Structure
After installation, Jenkins creates the following file structure:
```
jenkins_home/
├── config/
│ ├── config.xml
│ ├── global-security.xml
│ └── jenkins.model.JenkinsLocationConfiguration.xml
├── jobs/
│ └── <job_name>/
│ ├── config.xml
│ ├── nextBuildNumber
│ └── workspace
└── plugins/
└── <plugin_name>/
```
- The `jenkins_home` directory is the root directory of Jenkins. It contains all of the configuration files, job data, and plugins for Jenkins.

- The `config` directory contains the global configuration files for Jenkins. These files include security settings, plugin configurations, and more.

- The `jobs` directory contains the configuration and data for each created job. Each job has its own subdirectory under the `jobs` directory.

- The `plugins` directory contains all of the installed plugins for Jenkins. Each plugin has its own subdirectory containing the plugin files.

- The `workspace` directory is created when a job is executed. It is where the job's build takes place, and it contains the source code, build artifacts, and any temporary files generated during the build process.

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
