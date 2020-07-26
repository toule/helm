# Monitoring Public Repo Sample

## 가정 사항

- Elastic Kubernetes Service Engine Version: 1.15



## Basic Test

```bash
kubectl create namespace monitor
```

### Prometheus

#### Search

```bash
helm search repo prometheus
```

#### Install

```bash
helm install prometheus stable/prometheus
```

#### Result

![public-prometheus-sample](../../images/public-prometheus-sample.png)

#### Graph

```bash
kubectl port-forward svc/prometheus-server 8080:80 -n monitor
localhost:8080/targets
```

![public-prometheus-target](../../images/public-prometheus-target.png)

![public-prometheus-sample-1](../../images/public-prometheus-sample-1.png)

#### Pushgateway

```bash
export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace default port-forward $POD_NAME 9091
```

![public-prometheus-pushgateway](../../images/public-prometheus-pushgateway.png)

### Grafana

#### Search

```bash
helm search repo grafana
```

### Install

#### Edit file (path: grafana/values.yaml)

![public-grafana-sample-1](../../images/public-grafana-sample-1.png)

![public-grafana-sample-2](../../images/public-grafana-sample-2.png)

```bash
helm install grafana stable/grafana -f values.yaml -n monitor
```

### Result

![public-grafana-sample-1](../../images/public-grafana-sample-3.png)

- Console Login

```bash
export POD_NAME=$(kubectl get pods --namespace monitor -l "app.kubernetes.io/name=grafana,app.kubernetes.io/instance=grafana" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace monitor port-forward $POD_NAME 3000
```

- username: admin
- password

```bash
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

![public-granfa-sample-console-1](../../images/public-granfa-sample-console-1.png)

![public-granfa-sample-console-2](../../images/public-grafana-sample-5.png)