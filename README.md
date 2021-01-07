# Dashboard

![N|Solid](https://i.ibb.co/QcVg3gb/circle-cropped.png)

# custom dashboard

# ECS monitoring using Prometheus and Grafana
Setup ECS monitoring using Prometheus, Grafana, cAdvisor and Node Exporter

## Definations:
#### prometheus
Prometheus is pull base matrix collect , highly dimension data model.
#### cAdvisor
cAdvisor exposes container and hardware statistics as Prometheus metrics out of the box. By default, these metrics are served under the /metrics HTTP endpoint. ... To monitor cAdvisor with Prometheus, simply configure one or more jobs in Prometheus which scrape the relevant cAdvisor processes at that metrics endpoint.
#### node Exporter
The node exporter enables you to measure various machine resources such as memory, disk and CPU utilization. For installations from source you must install and configure it yourself.
#### grafana
Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources, 

## Setups Instructions:
1. Modify 'init-container' definition (in prometheus-grafana-definition.json) to download the correct 'prometheus.yml' configuration file.
2. Modify 'prometheus.yml' to make sure it queries and filters correct set of EC2 instance which needs to be monitored.

3. Use EC2 instance profile for ECS Cluster instances with permission to make describe calls for EC2 instances. This will be used by Prometheus to discover instance in your ECS cluster and add it in Prometheus targets  (http://monitor_ec2_public_ip:9090/targets).
4. Make sure instances in cluster can reach each other on ports 9090, 9100, and 9200 and open Grafana port 3000 for the IP range from where you need to access the Grafana Dashboard.

## Usages Instructions:

1. Create Task Definitions for cAdvisor, Node-Exporter, Prometheus and Grafana:
2. Create a DAEMON Service to run cAdvisor, Node-Exporter on every node in ECS Cluster:
3. Run one ECS Task for Prometheus and Grafana in the clsuter:
4. Access Grafana Dashboard using URL: http://ip:3000
   Use user:admin and password:admin to login and then reset the password.
5. After logginig in, add datasource
6. Useful Grafana Dashboards:
   - Docker Host Monitoring: 11074, 10619, 395
   - Docker Monitoring: 193
   - Docker monitoring with Node selection: 8321

