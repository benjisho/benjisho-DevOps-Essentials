# Exercise: Creating Dashboards with Grafana

In this exercise, you will learn how to create dashboards using Grafana. Grafana is a powerful open-source data visualization and monitoring tool that allows you to create customizable dashboards to gain insights into the performance and health of your systems. By the end of this exercise, you will have hands-on experience creating dashboards in Grafana.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Install Grafana](#step-1-install-grafana)
- [Step 2: Access Grafana](#step-2-access-grafana)
- [Step 3: Connect Grafana to Prometheus](#step-3-connect-grafana-to-prometheus)
- [Step 4: Create a Dashboard](#step-4-create-a-dashboard)
- [Step 5: Add Panels to the Dashboard](#step-5-add-panels-to-the-dashboard)
- [Step 6: Customize Dashboard and Panels](#step-6-customize-dashboard-and-panels)
- [Step 7: Share and Export Dashboards](#step-7-share-and-export-dashboards)

## Prerequisites
- Ubuntu machine
- Prometheus and Grafana installed and configured (refer to previous exercises)

## Step 1: Install Grafana

1. Open a terminal.

2. Download the latest version of Grafana from the official Grafana website (https://grafana.com/grafana/download?pg=get&plcmt=selfmanaged-box1-cta1).

3. Extract the downloaded archive to obtain the Grafana files.

4. Move the Grafana directory to a location in your system.

5. Start Grafana using the following command:
   ```
   ./bin/grafana-server
   ```
6. Grafana will start and be accessible through the default web interface at http://localhost:3000.
## Step 2: Access Grafana
1. Open a web browser and navigate to http://localhost:3000 (assuming you're accessing it on your local machine).

2. Log in to Grafana using the default credentials (admin/admin). You will be prompted to change the password.

3. After changing the password, you will be redirected to the Grafana home page.
## Step 3: Connect Grafana to Prometheus
1. Click on the "Configuration" gear icon on the left sidebar and select "Data Sources" from the menu.

2. Click on "Add data source" to add Prometheus as a data source.

3. Fill in the necessary information:

- Name: Give your data source a meaningful name (e.g., Prometheus).
- Type: Select "Prometheus" from the list.
- URL: Enter the URL of your Prometheus instance (e.g., http://localhost:9090).
- Access: Select "Server (Default)".
- Save and Test: Click on "Save & Test" to test the connection to Prometheus. You should see a "Data source is working" message.
## Step 4: Create a Dashboard
1. Click on the "+" icon on the left sidebar and select "Dashboard" from the menu.

2. Click on "Add new panel" to add panels to the dashboard.

3. Customize the dashboard by adding rows, changing panel sizes, and adjusting time ranges.

4. Save the dashboard by clicking on the "Save" icon at the top of the page.

## Step 5: Add Panels to the Dashboard
1. Click on "Add new panel" to add a panel to the dashboard.

2. Choose a visualization type from the available options, such as graphs, charts, or tables.

3. Configure the panel settings, including the data source (Prometheus), query, and visualization options.

4. Adjust the panel size, position, and other settings as needed.

5. Repeat the above ## Steps to add more panels to the dashboard.

## Step 6: Customize Dashboard and Panels
1. Use the Grafana editor to customize the dashboard layout, colors, and styles.

2. Explore additional panel settings and options to fine-tune the visualizations.

3. Configure alerts and thresholds for specific metrics or panels.

4. Save the changes to update the dashboard and panel configurations.

## Step 7: Share and Export Dashboards
1. Share your dashboard with others by clicking on the "Share" icon at the top of the page.

2. Generate a shareable link or embed the dashboard in external websites or applications.

3. Export the dashboard as a JSON file for backup or sharing purposes.

Congratulations! You have successfully created dashboards with Grafana. This exercise provides a foundation for visualizing and monitoring your data using Grafana's powerful features.
