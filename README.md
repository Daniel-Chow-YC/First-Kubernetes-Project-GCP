# Deploying Nodejs Sample App and MongoDB on GCP using Kubernetes

Aims:
- To use kubernetes on Google Cloud Platform to launch 2 clusters
  - A Frontend and a backend cluster
- The Frontend will have the nodejs sample app deployed with 3 replicas and a load balancer and should be accessible from a public IP
- The backend will have 3 mongodb replicas and an internal LoadBalancer which will connect the app to the DB

## Launching backend cluster
- ``export MY_ZONE=us-central1-a``
- ``gcloud container clusters create webbackend --zone $MY_ZONE --num-nodes 2``

### MongoDB deployments and Internal LoadBalancer
- create the mongodb_deploy.yml and mongodb_service.yml files

- ``kubectl apply -f mongodb_deploy.yml``
- ``kubectl apply -f mongodb_service.yml``

- Find the external IP of the mongodb service ``mongodb-svc``
  - run ``kubectl get svc``


## Launching Frontend cluster
- ``gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2``

### App Deployment and LoadBalancer
- create the app_deploy.yml and app_service.yml file

- replace ``mongodb-svc`` in ``value: "mongodb://mongodb-svc:27017/posts"`` with the external IP of the mongodb service ``mongodb-svc`` then
- ``kubectl apply -f app_deploy.yml``

- ``kubectl apply -f app_service.yml``
