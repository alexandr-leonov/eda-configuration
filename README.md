### K8s configuration for all components of Event Driven Architecture (EDA) pet project.

![](docs/Schema.png)


## Components repositories:

Order service: https://github.com/alexandr-leonov/eda-order-service

<br>
<br>

## Install infrastructure

```
# Set up 1 node k8s

> minikube start --memory=6000

# Go to environment folder

> cd dev

# install evnironment settings

> kubectl apply -f namespace.yaml
> kubectl apply -f secret.yaml

# install components

> kubectl apply -f postgres/postgres-cluster.yaml
> kubectl apply -f kafka/zookeeper-cluster.yaml
> kubectl apply -f kafka/kafka-borker.yaml

# install services
# (each service has CI config based on GitHub actions)

> kubectl apply -f services/order-service.yaml

# Create automate CD process with 4h refresh images policy
> kubectl apply -f system/rights.yaml
> kubectl apply -f system/scheduler.yaml

```


<br/>
<br/>

## K8s management console commands:

<br>

For get info about infrastructure item: 
```
kubectl -n (namesapce) get (deployments/statefulsets/services/pods)

Example: 

> kubectl -n postgres-cluster get pods
```

For get current ip / port: 
```
kubectl -n (namespace) get svc (service)

Example: 

> kubectl -n postgres-cluster get svc postgres-service
```

For get logs: 
```
kubectl -n (namespace) logs (pod)

Example: 

> kubectl -n postgres-cluster logs postgres-deployment-67f5fc7cdb-hsc4l
```

<br/>
<br/>


Create topics:
```
1) kubectl -n (namespace) exec -it (pod) bash
2) `script to create topic`

Example:

> kubectl -n "kafka-cluster" exec -it kafka-0 bash
> kafka-topics.sh --create --zookeeper zookeeper-service.kafka-cluster.svc.cluster.local:2181  --replication-factor 1 --partitions 1 --topic "order-topic"
```

Show topics:
```
> kubectl -n "kafka-cluster" exec -it kafka-0 bash
> kafka-topics.sh --list --bootstrap-server localhost:9092
```

Show all messages from topic:
```
> kubectl -n "kafka-cluster" exec -it kafka-0 bash
> kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic "order-topic" --from-beginning
```


## Links to materials:
- https://github.com/d1egoaz/minikube-kafka-cluster
- https://github.com/scriptcamp/kubernetes-jenkins
- https://kubernetes.io/docs/concepts/services-networking/service/#environment-variables
- https://stackoverflow.com/questions/52422300/how-to-schedule-pods-restart
- https://habr.com/ru/company/southbridge/blog/526130/