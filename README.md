# CS344-k8s-Group-Project
CS344 group project to create a 3 node KIND k8s cluster.




### c344_amd64.tar.gz
To load the build in terminal
- docker load -i c344_amd64.tar.gz

To run the build in terminal
- docker run --rm -p 8080:80 c344_amd64:latest


### To launch the cluster.yaml
- kind create cluster --config cluster.yaml

Confirm it's running:
- kubectl get nodes

To Remove Cluster
- kind delete cluster --name group-cluster