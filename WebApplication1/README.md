# Prerequisites

1. Install Docker for Windows
2. Activate Kubernetes in Docker for Windows options

#Build image (docker file is in the WebApplication1 project) :

`docker build -t k8s-prototype:v1 .

# Manual deploy :

`kubectl run k8s-prototype --image=k8s-prototype:v1 --port=80`

You can verify if app is deployed with `kubectl get pods` & `kubectl get deployments`

## Make app accessible :

kubectl expose deployment k8s-prototype --type=NodePort

You can now execute `kubectl get services` to see the port used by kubernetes to proxy the pods. You can access the app with

`http://localhost:{PORT_SHOWN_WITH_THE_COMMAND_ABOVE}/api/values`

# Automatic deploy :

`kubectl create -f deploy.yaml`

The yaml file contains the specs for the app. It will deploy two replica pods that contains nginx & the dotnet app.

# Auto recovery

run 

`kubectl get pods`

take the name of one of the pods and run :

`kubectl delete pod {NAME}`

running the next command will show you how kubernetes automatically spawns a new pod and pulling the docker image to keep the redundance of 2 replicas.

`kubectl describe pods`
