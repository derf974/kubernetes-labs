
# Kubernetes-labs : Deploiement d'un application PHP/redis
Basé sur ce tuto : [ici](https://cloud.google.com/kubernetes-engine/docs/tutorials/guestbook)


## Préparation de l'envirronement
```
docker run --rm -ti -v /Users/derf/.config/gcloud:/root/.config/gcloud -v $HOME/workspace/labs/kubernets/examples/guestbook:/apps google/cloud-sdk:alpine bash
```
## Configuration gcloud et le cluster

```
gcloud config set project labs-254314
gcloud config set compute/zone us-central1-b
gcloud container clusters create guestbook --num-nodes=3 --machine-type=f1-micro
gcloud container clusters list
```
## Installation et configuration de kubectl
```
gcloud components install kubectl
gcloud container clusters get-credentials guestbook
kubectl config current-context
```
## Installation et deploiement de l'application.
```
git clone https://github.com/kubernetes/examples.git
cd example/guestbook/
kubectl create -f redis-master-deployment.yaml
kubectl create -f redis-master-service.yaml
kubectl create -f redis-slave-deployment.yaml
kubectl create -f redis-slave-service.yaml

kubectl create -f frontend-deployment.yaml
kubectl create -f frontend-service.yaml

kubectl get service frontend

```

## Nettoyage:
```
kubectl delete service frontend
gcloud compute forwarding-rules list
gcloud container clusters delete guestbook
```
