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

# starting the Minikube cluster.

1) Start the Minikube cluster using the Docker driver:
   $ minikube start --driver=docker

2) Build the image inside Minikube’s Docker (no push to registry needed):
   $ eval $(minikube docker-env)
3) build the Docker image from the docker file.
   $ docker build -t python-k8s-app .
4) deployt the app to minikube:
   $ kubectl apply -f k8s/deployment.yaml
   $kubectl apply -f k8s/service.yaml
5) Access the App
   $ minikube service python-app-service
   This command will open your browser with the app URL like:
   http://127.0.0.1:30007
   You should see on your browser:
   Hello from Minikube!
# Congratulation you Successfully deplyed the simple Python app on minikube cluster.
Note: if you want to see the pods run: kubectl get pods

# now if you want to deploy Prometheus and grafana using Helm
1) Install Helm
   $ curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
   
2) then add Prometheus & Grafana Helm Repos
   $ helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   $ helm repo add grafana https://grafana.github.io/helm-charts
   $ helm repo update
   
3) Install Prometheus
   $ helm install prometheus prometheus-community/prometheus
   
4) Check it's running:
   $ kubectl get pods -l "release=prometheus"
   
5) Install Grafana
   $ helm install grafana grafana/grafana --set adminPassword='admin123'
7) Expose Grafana:
   $ kubectl port-forward svc/grafana 3000:80
   
Now open your browser: http://localhost:3000/
and put 🧑 Username: admin
🔐 Password: admin123
