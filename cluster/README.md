##Couchbase Clustering on Kubernetes

The files in this directory can serve as an example of how to deploy a cluster on Kubernetes. Tested on GKE as well as a self-deployed Kubernetes cluster.

###Usage
It should be noted at the beginning that this setup depends on KubeDNS to be enabled and functional to dsuccessfully deploy.

- Create the image with `docker build -t $DESIRED_IMG_NAME .`

- Update all .yml files with your new image name if necessary

- Create the master node with `kubectl create -f cluster-master.yml`. This file will provision a LoadBalancer for the WebUI of the master node as well.

- Once the master is up and LB has been provisioned, connect to the WebUI by going to `$LOADBALANCER_IP:8091` in your browser

- Create either auto-rebalancing nodes or just attach the nodes to the cluster with one of the two worker files:
```bash
kubectl create -f cluster-worker.yml

OR

kubectl create -f cluster-worker-rebalance.yml
```

- Scale workers with the normal scaling commands for Replication Controllers:
```
kubectl scale rc couchbase-worker-rebalance-rc --replicas=3
``
