# A simple K8 cluster
A kubernetes setup for a simple webapp that uses mongo DB. This application does not support persistent data for MongoDB. 

For the data to be persistent one needs to attach a volume and use StatefulSet instead of deployment for mongo db. 

Alternatively you can also use an external DB. To use external mongo DB instance the mongo-service can be modified as below.

 ```
 apiVersion: v1
 kind: Service
 metadata:
    name: mongo-service
 spec:
  selector:
    app: mongo
  ports:
    - name: http
      protocol: TCP
      port: 27017
      targetPort: 27017
    externalIPs:
    - 10.0.123.28
```
## Running on localhost
Checkout the code and follow the steps mentioned below. 
### Prerequisites
1. minikube should be installed
2. kubectl should be installed

### Update the secrets
Update the secrets in ```mongo-secret.yaml```
```
echo -n username | base64
echo -n password | base64
```
### Starting minikube
```minikube start```
### First time
```
kubectl apply -f mongo-config.yaml
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo.yaml
kubectl apply -f webapp.yaml
```
Run ```kubectl get all``` to confirm is everything is working fine. 

To open the web app in the browser we need to IP of the node. 
```minikube ip```

The web app should be up and running on ```http://minikubeip:30100```

## Some more commands
### To stop minikube
```minikube stop```
### To start minikube
```minikube start```

