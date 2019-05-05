# Deployment of ingress controller 

Ingress allows external users and outside client applications access to HTTP services. Ingress consists of two components: 
Ingress resource and Ingress controller and it is vital that both pieces are properly configured so that traffic can be routed from an outside client to a Kubernetes Service.
	Ingress resource is a collection of rules for the inbound traffic to reach Services. These are Layer 7 (L7) rules that allow hostnames (and optionally paths) to be directed to specific Services in Kubernetes
	Ingress controller acts upon the rules set by the Ingress Resource, typically via an HTTP or L7 load balancer.

Install Helm
```
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
```
chmod 700 get_helm.sh
```
./get_helm.sh
```
helm init

# Install Tiller
```
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
```
initialize Helm

helm init --service-account tiller --upgrade

We can see if tiller is running by checking for the tiller_deploy

kubectl get deployments -n kube-system

Deploying an NGINX Ingress Controller via Helm on our namespace 'tools'

helm install --namespace=tools --name nginx-ingress stable/nginx-ingress --set rbac.create=true 

Confirm that the nginx-ingress-controller Service has been deployed and that we have an external IP address associated with the service by running the following command:

kubectl get service nginx-ingress-controller -n tools

Configure Ingress Resource

An Ingress Resource object is a collection of L7 rules for routing inbound traffic to Kubernetes Services. Multiple rules can be defined in one Ingress Resource or they can be split up into multiple Ingress Resource manifests.

The Ingress Resource also determines which controller to utilize to serve traffic.

This can be set with an annotation, kubernetes.io/ingress.class, in the metadata section of the Ingress Resource.

annotations: kubernetes.io/ingress.class: nginx

kubectl apply -f ingress-resource.yaml

Verify that Ingress Resource has been created:

kubectl get ingress ingress-resource


