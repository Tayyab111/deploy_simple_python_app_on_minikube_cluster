# deploy_simple_python_app_on_minikube_cluster
I deployed the simple Python app on Minikube with Prometheus and Grafana. This guide will help you create a Minikube cluster to deploy a simple Python app running on port 5000, along with Prometheus and Grafana for monitoring. i) Prometheus is an open-source monitoring system that collects and stores metrics from your applications and infrastructure. It’s designed for reliability and scalability. ii) Grafana is a powerful visualization tool that lets you create dashboards and graphs based on data collected by Prometheus, helping you monitor and analyze your app’s performance visually.
# Prerequisites
Install Minikube: https://minikube.sigs.k8s.io/docs/start/

Install kubectl: https://kubernetes.io/docs/tasks/tools/

Install Docker: https://www.docker.com/get-started/

# the directory tree must be look like as below:
python-k8s-app/
├── app/
│   └── hello.py
├── Dockerfile
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
