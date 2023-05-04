# kubernetes-demo-app

Simple Kubernetes demo cluster with nodejs app

## Prerequisites

* Docker is recommended as minikube driver

## Minikube installation

Installation has been done via the [official documentation](https://minikube.sigs.k8s.io/docs/start/).

### Additional configuration

`sudo usermod -aG docker $USER && addgroup docker`

## Kubernetes

### Kubectl alias

`alias kubectl="minikube kubectl --"`

### Encoding secrets in base64

```bash
echo -n mongouser|base64
echo -n mongopassword|base64
```

### Deploying the kubernetes cluster

```bash
kubectl apply -f mongo-config.yml # Apply the config map first as it is a dependency to other deployments
kubectl apply -f mongo-secret.yml # Apply the secrets, since they are dependencies as well
kubectl apply -f mongo.yml # Deploy the mongodb pods
kubectl apply -f webapp.yml # Deploy the web app last, mongo is its dependency as well as the config map
```

#### Useful commands to verify cluster operation

```bash
kubectl get pod # Get pods status
kubectl get all # Get all objects
kubectl get configmap # Get config map
kubectl get secret # Get secrets
kubectl logs <POD ID> # See logs of certain pod
kubectl get service # Get services
minikube ip # Get minicube external IP
```
