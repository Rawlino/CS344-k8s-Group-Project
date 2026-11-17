# CS344-k8s-Group-Project
CS344 group project to create a 3 node KIND k8s cluster.

## Identification
- Team number: ###
- Team name: Giff & Sons
- Team members:
   - Connor Phelps
   - Gifferent Malquist
   - Lucas Lima
   - Caleb Dew
   - Sechan Jang
   - Orion Rawlings
- Project name: K8S Class Website

## Introduction
This project is a docker image of the Cybersecurity 344 class website that runs using KIND (Kubernetes in Docker). Its primary user-facing function is to serve the website.

The benefits of this project compared to a normal web server are mostly on the backend. This project provides load balancing and self healing. Load balancing decreases latency for users by distributing the network traffic across multiple nodes. Self healing enables the server to restart unresponsive/damaged nodes.

## Documentation

### Summary
This project uses KIND to run a k8s cluster on Docker. The website is bundled in an image called `c344_amd64.tar.gz`. Launching `cluster.yaml` launches the k8s cluster 

### How to run the project

#### c344_amd64.tar.gz
To load the build in terminal
```bash
docker load -i c344_amd64.tar.gz
```

To run the build in terminal
```bash
docker run --rm -p 8080:80 c344_amd64:latest
```

#### To launch the cluster.yaml

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
   This tells kubernetes to make the website accessible on port 80

7. To remove the cluster when finished:
   ```bash
   kind delete cluster --name group-cluster
   ```

### Concepts taught
This project can help teach the following:
- Using Docker
- Kubernetes integration with Docker (KIND)
- How web servers work
- Certain Kubernetes web server features

## Creation
### Goal
The goal of this project was to learn how to use KIND to create a server that implements many useful features for real-world servers.

### Process
We split the project into multiple different pieces including:

- Creating the `service.yaml`.
- Developing the demo to test the server.
- Creating the slides.
- Writing the documentation.

### Challenges
[Place challenges here]

### Sources
- [Kubernetes documentation](https://kubernetes.io/)
- ["Kubernetes Explained in 6 Minutes" by ByteByteGo](https://www.youtube.com/watch?v=TlHvYWVUZyc)
- [KIND Documentation](https://kind.sigs.k8s.io/docs/user/quick-start/)

### Tools
- Docker
- KIND
- Kubernetes
- Visual Studio Code
- Github
- yaml








### Orion's Demo Notes


Getting started
* Make sure 2 terminal tabs are open (or 2 terminal windows)
* In one, enter the command 'kubectl get pods -o wide -w' (this will give a live running update of the status of the nodes)

Testing Failure (In other terminal window)
* Enter command 'kubectl get pods -o wide' to get node id
* Enter command 'kubectl delete pod <node id>'
* Look at other window running the live status of the nodes to see the destruction and creation of a new node.

Testing Scaling
* Enter command 'kubectl scale deployment class-website --replicas=3'
* Now enter command 'kubectl get pods -o wide' to see that we now have 3 working nodes housing our website
* Enter command 'kubectl scale deployment class-website --replicas=2' to return to original configuration (use 'kubectl get pods -o wide' to showcase this again)

Testing working node failure (Deliberate on whether this is necessary)
