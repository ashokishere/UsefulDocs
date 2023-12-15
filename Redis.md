Install and Manage Redis, Prometheus, & Grafana on Kubernetes Using Helm
 
You already have a Kubernetes Cluster in place, but it does not come with Helm. You need to install Helm, using the installation steps from the official Helm website.



Go to the Helm website and find the installation instructions. Usually you can navigate to the menu like Docs, or Getting Started, and find the installation instructions


Open your Kubernetes terminal, and install Helm following the installation instructions from the Helm website.

Run the first command below to download the installation script.

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
Run the second command below to change the file permission, allowing the owner to read, write, and execute the file.

chmod 700 get_helm.sh
Run the script

./get_helm.sh

Make sure the installation is successful and Helm was installed by using this terminal command:

helm version

Resources
Documentation
You need to install Redis, a popular in-memory data store on Kubernetes cluster.

Find the Helm chart for Redis from the Helm artifact hub, and install it.

Make sure you can access Redis CLI and run a few Redis commands to make sure the installation is successful.



Go to the Helm artifact hub, and find the Redis Helm chart. There will be several charts available, but a good chart usually has more stars than the others. In this case, you can use Redis Helm chart from Bitnami provider


See the installation instruction



Copy paste command A (shown on step 2, red rectangle) to your Kubernetes cluster to add Helm repository which owns the Helm chart

helm repo add bitnami https://charts.bitnami.com/bitnami

Copy paste command B (shown on step 2, red rectangle) to your Kubernetes cluster to install the Helm chart. Wait for a moment for Helm to download and install. Notice here that the command uses specific version, which is usually the latest version. If need, you can specify a different version.

helm install my-redis bitnami/redis --version 17.11.2

Some applications provide post-installation guide for further processing. In this case, you can test the Redis installation using the guidance.

From the post-installation guide, run the commands to get Redis password, and run a Redis client. Follow these sequences:


Export Redis password to Kubernetes cluster

export REDIS_PASSWORD=$(kubectl get secret --namespace default my-redis -o jsonpath="{.data.redis-password}" | base64 -d)

Run a Redis client

kubectl run --namespace default redis-client --restart='Never'  --env REDIS_PASSWORD=$REDIS_PASSWORD  --image docker.io/bitnami/redis:7.0.11-debian-11-r7 --command -- sleep infinity

Connect to running Redis client terminal

kubectl exec --tty -i redis-client --namespace default -- bash

Connect to Redis server using the command from post-installation guide.


REDISCLI_AUTH="$REDIS_PASSWORD" redis-cli -h my-redis-master

Try to run several Redis commands to check that the installed Redis can be used

Set one data with key: my-key and value: my-dummy-value which will expire in 5 minutes

SET my-key my-dummy-value EX 300
Make sure that the key exists

KEYS my-key
Retrieve the value

GET my-key

Try to flush all keys using the following Redis command

FLUSHALL

This is a valid Redis command, but we can't use it. We will fix this issue later

Exit the Redis client and go back to Kubernetes CLI. Keep typing exit until going back to the main Kubernetes terminal


Resources
Documentation
Redis is no longer needed, so you need to remove it from the Kubernetes cluster.

Also, Kube-prometheus stack is currently installed on the namespace default. For a more structured work practice, you need uninstall the kube-prometheus stack and later re-install it on a different namespace.



List all of the installed Helm charts using the following command:

helm list
There are Redis and Kube-prometheus stack with the installation names shown in the green rectangle below


Remove installed Redis Helm chart by using the command below:

helm uninstall my-redis

Remove installed Kube-Prometheus stack Helm chart by using the command below:

helm uninstall my-kube-prometheus-stack

Re-list all installed Helm charts using the command below:

helm list
It should show nothing now meaning no Helm chart is left installed in the Kubernetes cluster.


Make sure you have no pods running on the namespace default, since the Helm charts were removed:

kubectl get pods -n default

Apparently, you still have redis-client, which is installed manually on Task 2 (not using a Helm chart). You can remove the Redis client pod by using the command below:

kubectl delete pod -n default redis-client

Re-check the pods, and you should have no pods now:

kubectl get pods -n default

Make sure you have no services on the namespace default, since the Helm charts are removed:

kubectl get services -n default
You only have kubernetes services itself, but no Redis nor Kube-prometheus related services, which means removal is succesful


Resources
Documentation
You need to install Prometheus, Grafana, and Alert Manager with these requirements:

installed on the namespace monitoring

installation name is solution-one-kube-prometheus

expose Prometheus using Ingress, on path /prometheus

expose Grafana using Ingress, on path /grafana

expose Alert Manager using Ingress, on path /alert-manager

You must use yml configuration file to fullfil the requirements.

Note : You already have Traefik Ingress controller on the Kubernetes cluster.



Go to the Helm artifact hub, and find the Kube-Prometheus Helm chart from the prometheus-community (same one in task #3)


On Kube-Prometheus stack Helm page, check the documentation, where you can see the possible configuration items by clicking the Default Values button



You will also find a link which will redirect you to the external documentation site


Where you can navigate further, to see how to expose Kube-Prometheus stack behind ingress controller.


The configuration is quite complex, but basically you will need to create a yaml file on the server containing the  items below:

prometheus:
  ingress:
    enabled: true
    annotations: 
      ingress.kubernetes.io/rewrite-target: /
    paths:
    - /prometheus
  prometheusSpec:
    routePrefix: /prometheus
 
grafana:
  adminPassword: changeme
  ingress:
    enabled: true
    annotations: 
      ingress.kubernetes.io/rewrite-target: /
    path: /grafana
  grafana.ini: 
    server:
      root_url: "%(protocol)s://%(domain)s:%(http_port)s/grafana"
      serve_from_sub_path: true
 
alertmanager:
  ingress:
    enabled: true
    annotations: 
      ingress.kubernetes.io/rewrite-target: /
    paths:
    - /alertmanager
  alertmanagerSpec:
    routePrefix: /alertmanager
These configurations define the settings for the Ingress resources, including path mappings, annotations, and specific configurations for Prometheus, Grafana, and Alertmanager within the kube-prometheus stack installation.

Let's break down the contents:

prometheus section:

ingress: create the Ingress resource for Prometheus.

annotations: Specifies annotations for the Ingress resource, including ingress.kubernetes.io/rewrite-target which rewrites the target URL path to "/".

paths: Defines the path(s) for the Ingress resource, in this case, "/prometheus".

prometheusSpec: Allows configuration of specific settings for Prometheus, such as routePrefix which sets the URL route prefix to "/prometheus".

grafana section:

ingress: create the Ingress resource for Grafana.

annotations: Specifies annotations for the Ingress resource, including ingress.kubernetes.io/rewrite-target which rewrites the target URL path to "/".

path: Defines the path for the Ingress resource, which is set to "/grafana".

grafana.ini: Configures settings for Grafana, such as root_url which specifies the base URL for Grafana and serve_from_sub_path to serve Grafana from a subpath.

alertmanager section:

ingress: create the Ingress resource for Alert manager.

annotations: Specifies annotations for the Ingress resource, including ingress.kubernetes.io/rewrite-target which rewrites the target URL path to "/".

paths: Defines the path(s) for the Ingress resource, in this case, "/alertmanager".

alertmanagerSpec: Allows configuration of specific settings for Alertmanager, such as routePrefix which sets the URL route prefix to "/alertmanager".

Go to the terminal, and create the file values-monitoring.yml using the following command:

nano values-monitoring.yml

Copy &  paste the configuration contents from Step 3:


Press CTRL-X (Windows) or Command-X (Mac), then Y


then Enter / Return to save the file and exit nano editor


Install Kube-Prometheus stack using custom configuration. Use this command:

helm install solution-one-kube-prometheus --repo https://prometheus-community.github.io/helm-charts kube-prometheus-stack --namespace monitoring --create-namespace --values values-monitoring.yml
Let's break down the command :

helm install: installs a Helm chart

solution-one-kube-prometheus: specifies the name to assign to the Helm release

--repo https://prometheus-community.github.io/helm-charts: specifies the repository from which the chart should be installed. In this case, it points to the Prometheus Community Helm Charts repository located at the provided URL. Helm will fetch the chart from this repository.

kube-prometheus-stack: specifies name of the chart you want to install

--namespace monitoring: specifies the namespace in which the chart will be installed. In this case, it's being installed in the monitoring namespace.

--create-namespace: instructs Helm to create the specified namespace if it doesn't already exist.

--values values-monitoring.yml: specifies a values file (values-monitoring.yml) to provide custom configurations for the chart during installation


Check that Kubernetes pods, services, and ingress, were created on the monitoring namespace

kubectl get pod -n monitoring | grep kube-prometheus

kubectl get service -n monitoring

kubectl get ingress -n monitoring

Try checking that the applications are accessible through ingress. Use curl to show only the HTTP response status code, as the response body will be long (HTML). The response status code should be 200 (meaning "OK")

curl -L -s -o /dev/null -w "%{http_code}\n" http://127.0.0.1/prometheus/metrics

curl -L -s -o /dev/null -w "%{http_code}\n" http://127.0.0.1/grafana

curl -L -s -o /dev/null -w "%{http_code}\n" http://127.0.0.1/alertmanager

Resources
Documentation
