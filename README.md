Monitoring and Alerting for an Application on AWS EKS
Project Overview
This project adds monitoring and alerting to an application running in an AWS EKS cluster. The goal was to extend the existing Kubernetes deployment from Project 2 with basic observability, so that the application’s health and resource usage can be monitored in real time.
The project focuses on setting up Prometheus and Grafana inside the cluster, creating a custom alert for application availability, and validating that the alert behaves correctly when the application state changes.
________________________________________
Environment and Setup
The application is deployed as a Kubernetes Deployment in an EKS cluster and exposed using a Kubernetes Service. On top of this setup, a monitoring stack was deployed into the cluster.
Prometheus is used to collect metrics from Kubernetes components and workloads, while Grafana is used to visualize those metrics. Both tools run inside the cluster and communicate using Kubernetes services.
________________________________________
Monitoring Implementation
The monitoring stack was installed into the EKS cluster using Helm, which is commonly used to deploy and manage Kubernetes applications.
The kube-prometheus-stack Helm chart was used to deploy Prometheus, Grafana, and the required Kubernetes metric exporters. Helm was chosen to simplify installation and ensure that all components were deployed with correct defaults and dependencies.
Once installed, Prometheus automatically started scraping metrics related to:
- pods and deployments
- CPU and memory usage
- replica availability
- namespace-level resource usage
Grafana dashboards were used to confirm that metrics were being collected correctly and to observe how the application behaves during normal operation.
________________________________________
Application Alerting
A custom Prometheus alert rule was created to monitor the availability of the application deployment. The alert checks how many replicas of the deployment are currently available and triggers when the number falls below a defined threshold for more than two minutes.
This alert was designed to show three possible states:
- inactive when the application is healthy
- pending when availability drops but the condition has not lasted long enough
- firing when the condition persists
________________________________________
Alert Testing and Validation
To test the alert, the deployment was intentionally modified to reduce the number of available replicas. This caused the alert to move from inactive to pending, and finally to firing after the configured time window.
The alert state changes were observed directly in the Prometheus UI. At the same time, Grafana dashboards were used to confirm that pod and resource metrics matched the application state.
Screenshots included in the repository show:
- the alert in inactive, pending, and firing states
- application resource usage in Grafana
- metrics collected from running pods
________________________________________
Project Scope
This project focuses only on monitoring and alerting. The application and cluster were already created in Project 2, and the CI/CD pipeline is intentionally not included here.
The purpose of this project is to demonstrate how a running Kubernetes application can be observed and how basic alerts can be added to detect availability issues.
________________________________________
What This Project Demonstrates
- deploying Prometheus and Grafana using Helm
- collecting Kubernetes and application metrics
- creating a custom Prometheus alert
- validating alert behavior by simulating application issues
- visualizing application health using Grafana dashboards

