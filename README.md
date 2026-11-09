# CS344-k8s-Group-Project
CS344 group project to create a 3 node KIND k8s cluster.




### c344_amd64.tar.gz
To load the build in terminal
- docker load -i c344_amd64.tar.gz

To run the build in terminal
- docker run --rm -p 8080:80 c344_amd64:latest


### To launch the cluster.yaml
# 1. Load the tar into local Docker
docker load -i c344_amd64.tar.gz

# 2. Create the kind cluster (from cluster.yaml)
kind create cluster --config kind/cluster.yaml

# 3. Load the image from Docker into your kind cluster!
kind load docker-image c344_amd64:latest --name group-cluster

# 4. Apply the deployment and service
kubectl apply -f kind/deployment.yaml
kubectl apply -f kind/service.yaml

# 5. Port-forward to view in browser at http://localhost:8080
kubectl port-forward service/class-website 8080:80

# 6. Confirm it's running:
- kubectl get nodes

# 7. To Remove Cluster
- kind delete cluster --name group-cluster