# edunext grafana dashboards

This repository contains three Grafana dashboards designed to monitor the performance and resource usage of Kubernetes clusters. Each dashboard focuses on different aspects of cluster operations, offering a clear and insightful view of the system's health and resource utilization.

## Dashboards

### 1. **Installations Performance**

This dashboard provides an overview of various metrics related to installations in the cluster. It includes panels displaying:

- Memory and CPU usage by deployment
- Available and unavailable replicas
- Pod states
- Ingress request volumes

The data is visualized using time series graphs, tables, and other formats to offer insights into deployment trends and resource utilization.

### 2. **Namespaces Performance**

This dashboard offers a comprehensive view of performance and resource usage across namespaces within the Kubernetes cluster. It includes:

- CPU and memory usage for each namespace and pod
- RAM usage in bytes and as a percentage of total cluster resources
- Kubernetes resorces count
- Storage usage
- Network transmission and reception metrics for each namespace

This helps monitor resource consumption and data traffic across the entire cluster.

### 3. **Nodes Performance**

This dashboard focuses on system performance across cluster nodes. Key metrics include:

- CPU utilization at both the node and cluster levels
- Memory usage compared to available resources
- Storage usage percentages
- Network traffic, including total data received and transmitted by each node

The dashboard offers a unified view of resource utilization, ensuring detailed monitoring of system health.

## Installation

If you use the official Grafana helm chart or kube-prometheus-stack, you can install the dashboards directly using the `dashboardProviders` and `dashboards` helm chart values.

```yaml
helmCharts:
- name: kube-prometheus-stack
repo: https://prometheus-community.github.io/helm-charts
version: xx.x.x
releaseName: prometheus
includeCRDs: true
valuesInline:
    grafana:
    dashboardProviders:
        dashboardproviders.yaml:
        apiVersion: 1
        providers:
        - name: 'edunext-grafana-dashboards'
            orgId: 1
            type: file
            disableDeletion: true
            editable: true
            options:
            path: /var/lib/grafana/dashboards/edunext-grafana-dashboards
    dashboards:
        edunext-grafana-dashboards:
        installations-performance:
            url: https://raw.githubusercontent.com/eduNEXT/edunext-grafana-dashboards/main/installations-performance.json
            token: ''
        nodes-performance:
            url: https://raw.githubusercontent.com/eduNEXT/edunext-grafana-dashboards/main/nodes-performance.json
            token: ''
        namespaces-performance:
            url: https://raw.githubusercontent.com/eduNEXT/edunext-grafana-dashboards/main/namespaces-performance.json
            token: ''
```