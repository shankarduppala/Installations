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
