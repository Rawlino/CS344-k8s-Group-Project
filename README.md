# CS344-k8s-Group-Project
CS344 group project to create a 3 node KIND k8s cluster.




### c344_amd64.tar.gz
To load the build in terminal
- docker load -i c344_amd64.tar.gz

To run the build in terminal
- docker run --rm -p 8080:80 c344_amd64:latest


### To launch the cluster.yaml

1. Load the tar into local Docker:
   ```bash
   docker load -i c344_amd64.tar.gz
   ```

2. Create the kind cluster:
   ```bash
   kind create cluster --config kind/cluster.yaml
   ```

3. Load the image from Docker into your kind cluster:
   ```bash
   kind load docker-image c344_amd64:latest --name group-cluster
   ```

4. Apply the deployment and service:
   ```bash
   kubectl apply -f kind/deployment.yaml
   kubectl apply -f kind/service.yaml
   ```

5. Confirm the nodes and pods are running:
   ```bash
   kubectl get nodes
   kubectl get pods
   ```

6. Port-forward to view in browser at http://localhost:8080:
   ```bash
   kubectl port-forward service/class-website 8080:80
   ```

7. To remove the cluster when finished:
   ```bash
   kind delete cluster --name group-cluster
   ```