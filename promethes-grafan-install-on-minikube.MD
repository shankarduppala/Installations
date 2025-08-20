Open minikube with driver, memory and cpu

            minikube start --driver=docker --momery=4096 --cpus=2

then check the nodes i.e minikube created or not

            kubect get nodes

then add the promethes repo by using helm charts

            helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
same way add grafan repo by using helm

            helm repo add grafana https://grafana.github.io/helm-charts

update the the repos once by using helm update

            helm repo update

Create the namespace using kubectl

            kubectl create namespace monitoring
            kubectl get ns

Install the promethes in monitoring namespace

            helm install prometheus prometheus-community/prometheus -n monitoring

install the grafana in the monitoring namespace

            helm install grafana grafana/grafana -n monitoring

Check the pods whather it's installed or not

            kubectl grt po -n monitoring

Expose the promethes frpm ClusterPort to Nodeport

            kubectl --namespace monitoring port-forward svc/prometheus-server 9090:80

Expose the grafana from ClusterPort to Nodeport

            kubectl --namespace monitoring port-forward svc/grafana 3000:80

Check the services 

            kubectl get svc -n monitoring

To get the password of grafana

            kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

if we want to put background 

            Start-Process powershell -ArgumentList "kubectl --namespace monitoring port-forward svc/prometheus-server 9090:80"
            Start-Process powershell -ArgumentList "kubectl --namespace monitoring port-forward svc/grafana 3000:80"

To access on web

            http://localhost:9090
            https://localhost 3000

In Grafana: Connections → Data Sources → Add Data Source
Choose Prometheus

            URL: http://prometheus-server.monitoring.svc.cluster.local
            Click Save & Test ✅

In Grafana sidebar → Dashboards → Import.
You can use these popular dashboard IDs from Grafana.com

            Node Exporter Full → 1860

            Kubernetes Cluster Monitoring (via Prometheus) → 315

            Prometheus 2.0 Overview → 3662

            K8s Pods/Deployment Monitoring → 6417




