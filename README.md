###K8s configuration for all components of Event Driven Architecture (EDA) pet project.




Links to materials:
- https://github.com/d1egoaz/minikube-kafka-cluster

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
> kafka-topics.sh --list --zookeeper zookeeper-service.kafka-cluster.svc.cluster.local:2181
```

Show all messages from topic:
```
> kubectl -n "kafka-cluster" exec -it kafka-0 bash
> kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic "order-topic" --from-beginning
```


