#Kubernetes Notes

# Build docker image
mvn spring-boot:build-image

# Run the sample project
docker run -p 8080:8080 spring-k8-demo:0.0.1-SNAPSHOT

# Test the service
curl localhost:8080/actuator/health

# Create Kubernets deployment file
kubectl create deployment demo --image=spring-k8-demo:0.0.1-SNAPSHOT --dry-run=client -o=yaml > deployment.yaml
echo --- >> deployment.yaml
kubectl create service clusterip demo --tcp=8080:8080 --dry-run=client -o=yaml >> deployment.yaml

# Deploy image to Kubernetes
kubectl apply -f deployment.yaml

Now you need to be able to connect to the application, which you have exposed as a Service in Kubernetes. One way to do that, which works great at development time, is to create an SSH tunnel:

#Expose Services
kubectl port-forward svc/demo 8080:8080

#Test the service in deployed Kubernetes
curl localhost:8080/actuator/health

# What is Kubernetes
Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation

# Namespace
In Kubernetes, namespaces provides a mechanism for isolating groups of resources within a single cluster.

# Pod
Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

A Pod (as in a pod of whales or pea pod) is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers.

# Deployment 
A Kubernetes deployment is a resource object in Kubernetes that provides declarative updates to applications. A deployment allows you to describe an application’s life cycle, such as which images to use for the app, the number of pods there should be, and the way in which they should be updated.

# Service
An abstract way to expose an application running on a set of Pods as a network service.
With Kubernetes you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods, and can load-balance across them.

# Config Maps
A ConfigMap is an API object used to store non-confidential data in key-value pairs. Pods can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a volume.

#Secrets
A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key. Such information might otherwise be put in a Pod specification or in a container image. Using a Secret means that you don't need to include confidential data in your application code.

#Volumes
On-disk files in a container are ephemeral, which presents some problems for non-trivial applications when running in containers. One problem is the loss of files when a container crashes. The kubelet restarts the container but with a clean state. A second problem occurs when sharing files between containers running together in a Pod.

# Kubernetes
# Create namespace
kubectl create namespace
# View running pods
kubectl get pods
# View container logs
kubectl logs -f [pod-name]  
e.g kubectl logs -f demo-96f6b7cc5-mk5rm
# Decribe pod
kubectl describe pod [pod-name]
# View deployments
kubectl get deployments
# Describe deployment
kubectl describe deployment [deployment-name]
# View services
kubectl get services
# Describe service
kubectl describe service [service-name]
# View secrets
kubectl get secrets
# Describe service
kubectl describe secret [secret-name]
# Get a shell to the running container
kubectl exec --stdin --tty [pod-name] -- /bin/bash
# Delete resources in the current namespace
kubectl delete all --all

# Kubernetes cheat sheet
https://kubernetes.io/docs/reference/kubectl/cheatsheet/ 

