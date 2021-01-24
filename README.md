![](/Redis.png)

# This process will create 6 Redis nodes as the Master-Slave architecture with docker-compose and kubernetes.

## For docker-compose file, we will create persisten volume in ```./data/redis_6379:/data```, just type
```docker-compose up -d```

## For Kubernetes, we will directly create 6 nodes and use a ConfigMap to allow to create Redis clusters.

```kubectl apply -f redis-configMap.yaml```

```kubectl apply -f redis-persistentVolumeClaim.yaml```

```kubectl apply -f redis-service.yaml```
```kubectl apply -f redis-service-ext.yaml```
```kubectl apply -f redis-statefulset.yaml```
Check the pods and IP:
```kubectl get pods -o wide```
Input the corresponding IP for each Pod in XXX
```kubectl exec -it redis-cluster-0 -- redis-cli --cluster create XXX:6379 XXX:6379 XXX:6379 XXX:6379 XXX:6379 XXX:6379 --cluster-replicas 1```
```kubectl apply -f redis-configMap.yaml```
Type: 'yes'
Check the cluster status:
```kubectl exec -it redis-cluster-0 -- redis-cli -c cluster nodes```
```kubectl exec -it redis-cluster-0 -- redis-cli cluster info```
Input `key` and `value` in Redis
```kubectl exec -it redis-cluster-0 -- redis-cli -c set key value```
