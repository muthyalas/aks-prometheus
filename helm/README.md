# Notes and Issues

## helm prometheus
```
helm install stable/prometheus
```

Notes:
* The Prometheus server can be accessed via port 80 on the following DNS name from within your cluster:
```
interested-kangaroo-prometheus-server.default.svc.cluster.local
```

* Get the Prometheus server URL by running these commands in the same shell:
```
export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=server" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace default port-forward $POD_NAME 9090
```

* The Prometheus alertmanager can be accessed via port 80 on the following DNS name from within your cluster:
```
interested-kangaroo-prometheus-alertmanager.default.svc.cluster.local
```

* Get the Alertmanager URL by running these commands in the same shell:
```
export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=alertmanager" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace default port-forward $POD_NAME 9093
```

* The Prometheus PushGateway can be accessed via port 9091 on the following DNS name from within your cluster:
```
interested-kangaroo-prometheus-pushgateway.default.svc.cluster.local
```

* Get the PushGateway URL by running these commands in the same shell:
```
export POD_NAME=$(kubectl get pods --namespace default -l "app=prometheus,component=pushgateway" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace default port-forward $POD_NAME 9091
```

## helm grafana
```
helm install stable/grafana
```
Notes:
* Get your 'admin' user password by running:
```
kubectl get secret --namespace default giggly-tortoise-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

* Get the Grafana URL to visit by running these commands in the same shell:
```
export POD_NAME=$(kubectl get pods --namespace default -l "app=giggly-tortoise-grafana,component=" -o jsonpath="{.items[0].metadata.name}")
kubectl --namespace default port-forward $POD_NAME 3000
```

* Configure grafana
https://medium.com/@timfpark/simple-kubernetes-cluster-monitoring-with-prometheus-and-grafana-dd27edb1641

### grafana dashboards
* [Kubernetes cluster monitoring (via Prometheus)](https://grafana.com/dashboards/315)
* [Kubernetes All Nodes](https://grafana.com/dashboards/3131)
* [Kubernetes App Metrics](https://grafana.com/dashboards/1471)
## helm rbac issue
* User "system:serviceaccount:kube-system:default" cannot get namespaces in the namespace "default"
https://github.com/kubernetes/helm/blob/master/docs/rbac.md
