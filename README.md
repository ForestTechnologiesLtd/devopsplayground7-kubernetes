### devopsplayground7-kubernetes
# Introduction to Kubernetes

## Overview

## Architecture

## Requirements

## Step 0 : Accessing the AWS instance
`ssh -i devops-playground.pem admin@<IP>`

## Step 1 : Installing **kubectl**
```
sudo wget https://storage.googleapis.com/kubernetes-release/release/v0.20.1/bin/linux/amd64/kubectl
sudo chmod u+x kubectl
sudo  mv kubectl /usr/local/bin/
```

To initialize the cluster : 
`sudo ./kube-up.sh`

## Step 2 : Run our first container from CLI
`sudo kubectl run nginx-base --image=nginx`

## Step 3 : Create a  Nginx *pod* template file and run a container from it
nginx-pod.yml:
```
apiVersion: v1
kind: Pod
metadata:
 name: nginx-web
 labels:
   app: nginx-web
spec:
 containers:
   - name: nginx-web
     image: nginx
```
`sudo kubectl create -f nginx-pod.yml`

`sudo kubectl run nginx-web --image=nginx`


## Step 4 : Scale the pod horizontally and load balance it
`sudo kubectl scale nginx-web --replicas=5`

## Step 5 : Expose the containers
`sudo kubectl expose nginx-web --port:80`

`curl <LB_IP>`

## Step 6 : Create a Tomcat *pod* template file
tomcat-pod.yml
```
apiVersion: v1
kind: Pod
metadata:
 name: tomcat
 labels:
   app: tomcat-web
spec:
 containers:
   - name: tomcat-web
     image: tomcat
```
`kubectl create -f tomcat-pod.yml`

`kubectl get pods`

## Step 7 : Do a Rolling Update of the whole pod
`sudo kubectl rolling-update nginx-web tomcat-web --image=tomcat-web`

`sudo kubectl get pods`

## Step 8 : Stop the cluster
