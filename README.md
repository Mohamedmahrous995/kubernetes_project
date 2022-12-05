# kubernetes_project

IN Frist we had to create secret.yaml object in order to make all kubernetes to get access to variables which is used to authenticate with db .
then  use this command in order to create secret object 
kubectl apply -f secret.yaml .  
we can check the secrets files which created in the whole cluster with this command  
kubectl get secret 

then we need to create mongodb deployment and service in the deployment object we had to specify all specific to mongo db container and use 
env variable and allow access to secet file .
then we had to use service for mongo db object and specify the target port for it so that all services in the cluster can access the mongo db pod through service 

this commands will help to some troubleshoot 
kubectl apply -f mongo.yaml .

the deployment and service object will be created 
useful commands to check status of deployment and service ..........
kubectl get pod 
kubectl get deployment 
kubectl get service 
we can use this attributes either
kubectl get pod "pod-name" -o yaml 
kubectl describe pod "pod-name"
kubectl describe deployment "deployment Name"

in case you wanna see logs for pod and deployment
kubectk logs "pod Name"
kubectk logs deployment\"deployment-name"

in case that our deployment and service succedded we nw had to create another deployment and service for mongo express 
but frist we need to know how mongo express get acess to mongo db 
- there is variables in secret file which we had to specify them in container specification 
- but still some thing missing  ( db url "mongodb-service")
- this kinda a global variable which we had to specify it and refer to it from a globale config file 

HERE configMap turn is com to specify global variable which
kubectl apply -f mongo-configmap.yaml .

so that deployment can read data from secret and configmap object 

the reason for configmap and secret file had to be together that there is a credentials hat to be anaonymous to all user so that we use secret 
and config file to create and maintaine global variables which is no problem if any one know these variables and values .

Expose service to the internet 
in mongo express service we had to specify 
type: LoadBalancer  or NodePort 
and the node port port which we will access it through the browser .

in case you use minikube you had to expose the service through this command 
minikube service list 
or minikube service "service Name"
it will give you url with port you specified before use it in the browser and it should be working .

In Case we had to use domaine name and made our cluster more secure 
we can use Ingress controller to route the traffic inside oure cluster 

so we had to enable ingress in oure cluster 
 minikube addons enable ingress
 kubectl get pods -n ingress-nginx
then use ingress object with the specific configuration in order to run our website 
kubectl apply -f ingress.yaml 




**** the end ****

 
 
 



















