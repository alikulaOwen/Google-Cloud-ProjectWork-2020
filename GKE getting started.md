# Google Cloud Fundamentals: Getting Started with GKE
## Overview
you create a Google Kubernetes Engine cluster containing several containers, each containing a web server. You place a load balancer in front of the cluster and view its contents.

## Objectives
you will perform the following tasks:

-   Provision a  Kubernetes cluster using  Kubernetes Engine.
    
-   Deploy and manage Docker containers using  `kubectl`.

## Step  1: Sign in to the Google Cloud Platform (GCP) Console
## Step 2: Confirm that needed APIs are enabled
1.  Scroll down in the list of enabled APIs, and confirm that both of these APIs are enabled:
    -   Kubernetes Engine API
    -   Container Registry API
## Step 3: Start a Kubernetes Engine cluster
1.  in the gcp commandline assign zone closest to you into the environment variable MY_ZONE
```
export MY_ZONE=
```
2. followed by the zone that Qwiklabs assigned to you. Your complete command will look similar to this:
```
export MY_ZONE=us-central1-a
```
3.  Start a Kubernetes cluster managed by Kubernetes Engine. Name the cluster  **webfrontend**  and configure it to run 2 nodes:
   ```
    gcloud container clusters create webfrontend --zone $MY_ZONE --num-nodes 2

```
It takes several minutes to create a cluster as Kubernetes Engine provisions virtual machines for you.
After creating the kubernetes has been created, check your installed version of Kubernetes using the  `kubectl version`  command:
```
kubectl version
```

The  `gcloud container clusters create`  command automatically authenticated  `kubectl`  for you.
after that you can check in the console Vm instance you will see that Kubernetes cluster is now ready for use.

## Task 4: Run and deploy a container
launch a single instance of the nginx container.
```
kubectl create deploy nginx --image=nginx:1.17.10
```

all containers are running in pods. This use of the  `kubectl create`  command caused Kubernetes to create a deployment consisting of a single pod containing the nginx container. In this command, you launched the default number of pods, which is 1.

2.  View the pod running the nginx container:
       ```
        
    kubectl get pods
     ```
    
3.  Expose the nginx container to the Internet:
    
    ```
    kubectl expose deployment nginx --port 80 --type LoadBalancer
    
    ```
    
    Kubernetes created a service and an external load balancer with a public IP address attached to it. The IP address remains the same for the life of the service. Any network traffic to that public IP address is routed to pods behind the service: in our case, the nginx pod.
    2.  View the new service:
    
    ```
    kubectl get services
    
    ```
    
    You can use the displayed external IP address to test and contact the nginx container remotely.
    
    It may take a few seconds before the  **External-IP**  field is populated for your service. Just re-run the  `kubectl get services`  command every few seconds until the field is populated.
    
4.  Open a new web browser tab and paste your cluster's external IP address into the address bar. The default home page of the Nginx browser is displayed.
    
5.  Scale up the number of pods running on your service:
    
    ```
    kubectl scale deployment nginx --replicas 3
    
    ```
    
    Scaling up a deployment is useful when you want to increase available resources for an application that is becoming more popular.
    
6.  Confirm that Kubernetes has updated the number of pods:
    
    ```
    kubectl get pods
    
    ```
    
7.  Confirm that your external IP address has not changed:
    
    ```
    kubectl get services
    
    ```
    
8.  Return to the web browser tab in which you viewed your cluster's external IP address. Refresh the page to confirm that the nginx web server is still responding.
9. You are done