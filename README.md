# eda-configuration

**Configuration of EDA project (LB, Deploy, ...)**

*K8s configuration for all components of Event Driven Architecture (EDA) project.*

Links to materials:
- https://github.com/d1egoaz/minikube-kafka-cluster

K8s management console commands:

For get info about infrastructure item: 
```
kubectl -n (namesapce) get (deployments/statefulsets/services/pods)
Example: kubectl -n postgres-cluster get pods
```

For get current ip / port: 
```
kubectl -n (namespace) get svc (service)
Example: kubectl -n postgres-cluster get svc postgres-service
```

For get logs: 
```
kubectl -n (namespace) logs (pod)
Example: kubectl -n postgres-cluster logs postgres-deployment-67f5fc7cdb-hsc4l
```
