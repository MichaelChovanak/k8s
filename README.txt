This project sets up a simple k8s app using MongoDB for a backend 
and MongoExpress for an admin interface to the backend.

I used minikube for simplicity, so start it with:
```
minikube start
```

To start the app, first move to configs directory:
```
cd configs
```

Next, create the Secret and ConfigMap instances:
```
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo-configmap.yaml
```
The Secret stores the admin username and password in base64,
which other services can access for authentication into DB.
The config map is used by the mongo-express service to retrieve 
the database url.

With the dependencies done, we now create the mongoDB database
and mongo-express services:
```
kubectl apply -f mongo.yaml
kubectl apply -f mongo-express.yaml
```
This sets up the backend and frontend.

Finally, we generate an external ip using mongo-express with:
```
minikube service mongo-express-service
```
This will open the external admin interface in the browser,
which we can use to modify the DB.
