# Exercise: Implementing Monitoring with Prometheus

In this exercise, you will learn how to implement monitoring using Prometheus. Prometheus is a popular open-source monitoring and alerting solution that specializes in time-series data collection, querying, and alerting. By the end of this exercise, you will have hands-on experience setting up Prometheus to monitor your applications and infrastructure.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Install Prometheus](#step-1-install-prometheus)
- [Step 2: Configure Prometheus](#step-2-configure-prometheus)
- [Step 3: Collect Metrics with Prometheus](#step-3-collect-metrics-with-prometheus)
- [Step 4: Query Metrics with Prometheus](#step-4-query-metrics-with-prometheus)
- [Step 5: Set up Alerting with Prometheus](#step-5-set-up-alerting-with-prometheus)

## Prerequisites

- An Ubuntu machine/container to install and run Prometheus.
- Basic understanding of monitoring concepts such as metrics, time-series data, and alerting.
   - This will help you to better understand, configure and use Prometheus for monitoring your applications and infrastructure.

## Step 1: Install Prometheus

1. Open a terminal.

2. Download the latest version of Prometheus from the official Prometheus website (https://prometheus.io/download/#prometheus).

3. Extract the downloaded archive to obtain the Prometheus binary.
   ```
   tar xvfz prometheus-*.tar.gz
   ```
4. Move the Prometheus binary to a directory in your system's `PATH` to make it executable.
   - Identify the directories in your system's `PATH` where executables are commonly stored. Some common directories include `/usr/local/bin` and `/usr/bin`. You can check the contents of your `PATH` variable by running the command:
     ```
     echo $PATH
     ```

   - Move the Prometheus binary to one of the directories in your PATH. For example, if you want to move it to /usr/local/bin, you can use the following command:
     ```
     sudo mv prometheus /usr/local/bin/
     ```
     Note: You may need to use sudo or run the command as the root user depending on the permissions of the destination directory.
     - Once the binary is moved, you should be able to run the prometheus command from anywhere in your terminal.
     - By moving the Prometheus binary to a directory in your system's PATH, you make it accessible as an executable command. This allows you to run prometheus without specifying the full path to the binary.
5. Verify the Prometheus installation by running the following command:
   ```
   prometheus --version
   ```
6. You should see the Prometheus version displayed in the output.

## Step 2: Configure Prometheus
1. Create a configuration file named prometheus.yml to define the Prometheus configuration.
   - Typically the Prometheus configuration file (prometheus.yml) is located in the `/etc/prometheus/` directory.
     However, the exact location may vary depending on your installation method or configuration.
   - To locate the prometheus.yml file, you can try the following steps:
      - Open a terminal.
      - Navigate to the /etc/prometheus/ directory by running the command:
        ```
        cd /etc/prometheus/
        ```
      - Check if the prometheus.yml file is present in the current directory by running the command:
        ```
        ls prometheus.yml
        ```
        If the file exists, you will see its name listed in the output.
      - If the prometheus.yml file is not located in the /etc/prometheus/ directory, you may need to search for it in other locations based on your installation or configuration. You can try searching for the file using the find command:
        ```
        sudo find / -name prometheus.yml
        ```
        This command will search the entire filesystem (/) for any file named prometheus.yml and display the paths where it is found.
2. Specify the scrape configuration to determine the targets from which Prometheus should collect metrics. For example:
   - This will configure Prometheus to monitor itself
   ```
   global:
     scrape_interval: 15s
   
     external_labels:
       monitor: 'codelab-monitor'
   
   scrape_configs:
     - job_name: 'prometheus'
       scrape_interval: 5s
       static_configs:
         - targets: ['localhost:9090']
   ```
3. Configure additional settings such as retention policies, alerting rules, and recording rules based on your monitoring requirements.

4. Verify the syntax of the Prometheus configuration by running the following command:
   ```
   promtool check config prometheus.yml
   ```
   You should see a "SUCCESS" message if the configuration syntax is valid.

5. Save the prometheus.yml configuration file.

6. Start Prometheus using the following command:
   ```
   prometheus --config.file=prometheus.yml
   ```
7.Prometheus will start and begin collecting metrics based on the configured targets.

## Step 3: Collect Metrics with Prometheus
1. Instrument your applications or infrastructure to expose metrics in a format that Prometheus can understand. You can use Prometheus client libraries or exporters for various systems and services.

2. Configure your applications or services to expose metrics on a designated endpoint, such as /metrics.

3. Prometheus will scrape the configured targets and collect the exposed metrics based on the defined scrape configuration.

## Step 4: Query Metrics with Prometheus
1. Open a web browser and navigate to the Prometheus web interface (http://localhost:9090).

2. Use the Prometheus Query Language (PromQL) to explore and query the collected metrics. For example:
   ```
   http_requests_total
   ```
3. Execute queries to retrieve and aggregate metrics based on your monitoring requirements.

4. Utilize PromQL functions and operators to perform advanced data analysis and visualization.

## Step 5: Set up Alerting with Prometheus
1. Create an alerting rules file named alert.rules.yml to define alerting rules for Prometheus.

2. Specify alerting rules based on metric thresholds or other conditions. For example:
   ```
   groups:
     - name: example
       rules:
         - alert: HighErrorRate
           expr: http_errors_total > 100
           for: 5m
           labels:
             severity: critical
           annotations:
             summary: High error rate detected
             description: The application is experiencing a high rate of errors.
   ```
3. Configure alertmanager to receive and manage alerts generated by Prometheus.

4. Reload Prometheus configuration using the following command:
   ```
   prometheus --config.file=prometheus.yml --web.enable-admin-api=1 --web.enable-lifecycle=1 --alertmanager.url=http://localhost:9093
   ```
5. Prometheus will monitor the configured metrics and trigger alerts based on the defined alerting rules.

Congratulations! You have successfully implemented monitoring with Prometheus. This exercise provides a foundation for monitoring your applications and infrastructure using Prometheus.
