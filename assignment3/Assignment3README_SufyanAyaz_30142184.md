# Assignment 3 Steps and Outputs - Sufyan Ayaz - 30142814

Here is the README that will outline all the steps I have taken, and the outputs I have achieved (as well as the outputs anyone else running this should achieve).

## **_Step 1_** - Getting Started

1. Alright, to start off, the first thing you are going to do is `cd` into the directory where all the files are as follows:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2 (main) $ cd assignment3/
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>

2. Once inside the appropriate directory (which is the "assignment3" directory for me), run the command `minikube start` to enter the minikube simulated kubernetes environment. Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ minikube start
😄  minikube v1.32.0 on Ubuntu 20.04 (docker/amd64)
✨  Using the docker driver based on existing profile
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
🔄  Restarting existing docker container for "minikube" ...
🐳  Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.9.4
🔎  Verifying ingress addon...
🌟  Enabled addons: storage-provisioner, default-storageclass, ingress
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $
```

<br>

## **_Step 2_** - Starting the NGINX Load Balancer and the Apps

1. After the simulated kubernetes environement is setup and running, execute the commands necessary to create all the resources for the nginx load balancer. The commands, which will be run in the stated order, are `kubectl create -f nginx-configmap.yaml `, `kubectl create -f nginx-svc.yaml`, `kubectl create -f nginx-dep.yaml`, and `kubectl create -f nginx-ingress.yaml`. Here is what the output of running these command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f nginx-configmap.yaml 
configmap/nginx-configmap created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f nginx-svc.yaml 
service/nginx-svc created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f nginx-dep.yaml 
deployment.apps/nginx-dep created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f nginx-ingress.yaml 
ingress.networking.k8s.io/nginx-ingress created 
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>

> After running these commands, the nginx load balancer should be setup and ready to begin routing any requests that heading to the app servers.


<br>

2. Once the nginx load balancer is good to go, it is now time to setup the resources for app-1 and app-2. In order to create the resources for app-1 and app-2, the following commands, in the stated order, will be run: `kubectl create -f app-1-svc.yaml`, `kubectl create -f app-1-dep.yaml`, `kubectl create -f app-1-ingress.yaml`, `kubectl create -f app-2-svc.yaml`, `kubectl create -f app-2-dep.yaml`, and `kubectl create -f app-2-ingress.yaml`. Here is what the output of running these command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f app-1-svc.yaml 
service/app-1-svc created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f app-1-dep.yaml 
deployment.apps/app-1-dep created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f app-1-ingress.yaml 
ingress.networking.k8s.io/app-1-ingress created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f app-2-svc.yaml 
service/app-2-svc created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f app-2-dep.yaml 
deployment.apps/app-2-dep created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl create -f app-2-ingress.yaml 
ingress.networking.k8s.io/app-2-ingress created
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```

<br>

> After running these commands, app-1 and app-2 should be setup and ready to begin receiving and responding to requests.

<br>

## **_Step 3_** - Perliminary Commands to Execute Before Things Can Be Run

After all the resources are created, and before we can begin curling, you need to execute a few commands to make sure everything runs smoothly.
<br>

1. The first command to execute is `minikube addons enable ingress`, which will enable the addon necessary for allowing the ingress resources to run properly. Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ minikube addons enable ingress
💡  ingress is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.9.4
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
🔎  Verifying ingress addon...
🌟  The 'ingress' addon is enabled
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>

2. The second command to execute is `kubectl get po`. This will allow you to ensure that all the pods needed are created. There should be 5 nginx pods, 1 app-1 pod, and, 1 app-2 pod. Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl get po
NAME                         READY   STATUS    RESTARTS       AGE
app-1-dep-86f67f4f87-wbncc   1/1     Running   0              103s
app-2-dep-7f686c4d8d-nfj4p   1/1     Running   0              90s
nginx-dep-5d69b6994-9h5gn    1/1     Running   3 (116s ago)   2m12s
nginx-dep-5d69b6994-qsmgh    1/1     Running   3 (114s ago)   2m12s
nginx-dep-5d69b6994-vcd9n    1/1     Running   3 (113s ago)   2m12s
nginx-dep-5d69b6994-vntp6    1/1     Running   3 (113s ago)   2m12s
nginx-dep-5d69b6994-wxtms    1/1     Running   3 (114s ago)   2m12s
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>

3. The third command to execute is `minikube ip`. This will provide the ip address for the kubernetes environment that is necessary for running the curl command propery in the simulated environment. Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ minikube ip
192.168.49.2
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>

## **_Step 4_** - Run Everything

Now that everything is setup and ready, we can begin sending requests to the nginx load balancer, which will redirect the requests to the apps. In order to send these requests the following command needs to be executed: `curl http://192.168.49.2/`. 
<br>

> Note: The ip address used in the curl command (which in my case was "192.168.49.2") is the one provided by executing the `minikube ip` command.

<br>
Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-1-dep-86f67f4f87-wbncc]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-1-dep-86f67f4f87-wbncc]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-2-dep-7f686c4d8d-nfj4p]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-1-dep-86f67f4f87-wbncc]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-1-dep-86f67f4f87-wbncc]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-2-dep-7f686c4d8d-nfj4p]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-2-dep-7f686c4d8d-nfj4p]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-1-dep-86f67f4f87-wbncc]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-1-dep-86f67f4f87-wbncc]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://192.168.49.2/
Hello World from [app-1-dep-86f67f4f87-wbncc]!
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>

> Note, as you can see in the above provided output, the curl command was executed 10 times, and of those 10 executions, 7 returned a response from app-1 and 3 returned a response from app-2. This is due to the fact that the nginx load balancer resources and the apps resources are set up so that 70% of the requests are redirected to the main deployment set as app-1 , and 30% of the requests are redirected to the canary deployment set as app-2.

<br>

## **_Step 5_** - Finish

Now that the load balancer and the apps have been tested, the simulated environment needs to be cleaned up before it can be closed.
<br>

1. The first command to execute when cleaning up is `minikube addons disable ingress`, to disable the ingress addon. Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2 (main) $ minikube addons disable ingress
🌑  "The 'ingress' addon is disabled"
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>

2. The second command to execute when cleaning up is `kubectl delete -f .`, to destroy all the resources that were created for the nginx load balancer, app-1, and app-2. Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl delete -f .
deployment.apps "app-1-dep" deleted
ingress.networking.k8s.io "app-1-ingress" deleted
service "app-1-svc" deleted
deployment.apps "app-2-dep" deleted
ingress.networking.k8s.io "app-2-ingress" deleted
service "app-2-svc" deleted
configmap "nginx-configmap" deleted
deployment.apps "nginx-dep" deleted
ingress.networking.k8s.io "nginx-ingress" deleted
service "nginx-svc" deleted
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $  
```
<br>

3. The final command to execute when cleaning up is `minikube stop`, to stop the simulated kubernetes environment created to run this assignment. Here is what the output of running this command should look like:

```bash
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ minikube stop
✋  Stopping node "minikube"  ...
🛑  Powering off "minikube" via SSH ...
🛑  1 node stopped.
@SufyanAyaz ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
<br>
Now that everything is cleaned up, the codespace can be closed.

## Fin.