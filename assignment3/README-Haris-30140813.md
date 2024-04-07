# Haris (30140813) Assignment 3 Steps and Outputs

## **Step 1** - Initial

first, go into the working directory as follows:

```bash
 cd assignment3/
```
<br>

Run the following command to start minikube:

```bash
minikube start
```

<br>

Then run the following command to enable ingress:

```bash
minikube addons enable ingress
```

<br>

It should look like the following after doing the above:

```bash
@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2 (main) $ cd assignment3/
@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ minikube start
😄  minikube v1.32.0 on Ubuntu 20.04 (docker/amd64)
✨  Automatically selected the docker driver. Other choices: none, ssh
📌  Using Docker driver with root privileges
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
💾  Downloading Kubernetes v1.28.3 preload ...
    > preloaded-images-k8s-v18-v1...:  403.35 MiB / 403.35 MiB  100.00% 117.77 
    > gcr.io/k8s-minikube/kicbase...:  453.90 MiB / 453.90 MiB  100.00% 69.36 M
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.28.3 on Docker 24.0.7 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🔎  Verifying Kubernetes components...
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ minikube addons enable ingress
💡  ingress is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
    ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.9.4
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
    ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20231011-8b53cabe0
🔎  Verifying ingress addon...
🌟  The 'ingress' addon is enabled
@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $
```

<br>

## **Step 2** - Start Services

Run the following command to start all the services:

```bash
kubectl apply -f .
```

<br>

Check if the services are running using any of the following command:

```bash
kubectl get ingresses
```
```bash
kubectl get pods
```
```bash
kubectl get deployments
```
<br>

The outputs should like the following:

```bash
@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl apply -f .
deployment.apps/app-1-dep created
ingress.networking.k8s.io/app-1-ingress created
service/app-1-svc created
deployment.apps/app-2-dep created
ingress.networking.k8s.io/app-2-ingress created
service/app-2-svc created
configmap/nginx-configmap created
deployment.apps/nginx-dep created
ingress.networking.k8s.io/nginx-ingress created
service/nginx-svc created
@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ kubectl get pods
NAME                         READY   STATUS    RESTARTS      AGE
app-1-dep-86f67f4f87-pfgq2   1/1     Running   0             32m
app-2-dep-7f686c4d8d-rh5tn   1/1     Running   0             32m
nginx-dep-5d69b6994-4ssj6    1/1     Running   7 (26m ago)   32m
nginx-dep-5d69b6994-g7xsd    1/1     Running   7 (26m ago)   32m
nginx-dep-5d69b6994-gd4zj    1/1     Running   7 (26m ago)   32m
nginx-dep-5d69b6994-vsh8n    1/1     Running   7 (26m ago)   32m
nginx-dep-5d69b6994-whbns    1/1     Running   7 (26m ago)   32m
```

<br>

## **Step 3** - Checking functionality by running curl

Now, run the following command to check whether the traffic is being directed correctly:

```bash
curl http://$(minikube ip)/
```

<br>

The output should something like the following:

```bash
@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-pfgq2]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-pfgq2]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-pfgq2]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-2-dep-7f686c4d8d-rh5tn]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-pfgq2]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-pfgq2]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-2-dep-7f686c4d8d-rh5tn]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-2-dep-7f686c4d8d-rh5tn]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-pfgq2]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ curl http://$(minikube ip)/
Hello World from [app-1-dep-86f67f4f87-pfgq2]!@HarisKashif ➜ /workspaces/ensf400-lab8-kubernetes-2/assignment3 (main) $ 
```
The command was ran 10 times. We can see that the traffic was directed to `app-1` 7 out of 10 times. And was directed to `app-2` 3 out of 10 times. This suggests that it is working correctly. Although traffic will not always be directed exactly 70% to `app-1` and 30% to `app-2`, it will generally be true and will become more accurate as `curl http://$(minikube ip)/ `  is ran more times.
<br>

## **Step 4** - Finish

Finally, run the following commands to delete all pods and stop minikube:

```bash
kubectl delete -f .
```
```bash
minikube stop
```

<br>