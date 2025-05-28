# Monitoring-AKS
In my organization we have AKS setup where we have deployed multiple application. In order to monitor it we have implemented Grafana + Prometheus for colling metrics and visualising it on Grafana.

Promethues will collect **Real-time metrics from pods, nodes, and containers**


**Step 1: Install Prometheus and Grafana using helm charts**
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install monitoring prometheus-community/kube-prometheus-stack \
  --namespace mon \
  --create-namespace

**Step 2: Change the service type of Grafana from ClusterIP to LoadBalancer to expose the Grafana UI**

**Step 3: Go to Grafana and add prometheus as a data source**

**Step 4: Alternatively, you can change the config of prometheus as needed**
