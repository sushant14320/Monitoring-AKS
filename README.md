######################### **Monitoring-AKS** ################################################################################
In my organization we have AKS setup where we have deployed multiple application. In order to monitor it we have implemented Grafana + Prometheus for collecting metrics and visualising it on Grafana.

Promethues will collect **Real-time metrics from pods, nodes, and containers**


**Step 1: Install Prometheus and Grafana using helm charts**
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

helm install monitoring prometheus-community/kube-prometheus-stack \
  --namespace mon \
  --create-namespace

**Step 2: Change the service type of Grafana from ClusterIP to LoadBalancer to expose the Grafana UI**
kubectl edit svc monitoring-grafana -n mon


**Step 3: Go to Grafana and add prometheus as a data source**

**Step 4: Alternatively, you can change the config of prometheus as needed**
helm show values prometheus-community/kube-prometheus-stack > values.yaml



######################### **Monitoring application logs** ################################################################################
In order to monitor application losg stored at custom path inside container, weuse Loki + Promtail setup and viualize it on Grafana.


**Step 1: Install Loki using helm with grafana and promtail disabled**
The reason why grafana and promtail are disabled because we are using Azure managed Grafana and custom config of promtail


**Step 2: create a ConfigMap for promtail config which contains scrape configs**
This is will tell promtail from where ( directory ) to scrape logs


**Step 3: Edit the loki service from ClusterIP to Grafana**
This will be useful whil adding Loki as data source to Grafana
