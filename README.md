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

