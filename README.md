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
