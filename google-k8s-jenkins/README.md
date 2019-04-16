# What is Jenkins

Jenkins is an open source automation tool written in Java with plugins built for Continuous Integration purpose. Jenkins is used to build and test your software projects continuously making it easier for developers to integrate changes to the project, and making it easier for users to obtain a fresh build. It also allows you to continuously deliver your software by integrating with a large number of testing and deployment technologies.

## Setup Jenkins On Kubernetes Cluster

1.Create a Namespace
```   
 kubectl create ns tools
```
2.Create a deployment yaml and deploy it
```
 kubectl create -f jenkins-deployment.yaml --namespace=tools
```
3.Now, you can get the deployment details using the following command
```
 kubectl  describe deployments --namespace=tools
```
4.You can create a Persisten Volume. (PV) is a piece of storage in the cluster that has been provisioned by an administrator. This API object captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system.
```
 kubectl create -f jenkins-pv.yaml
```
5.Create Persistent Voulme Claim. (PVC) is a request for storage by a user and allow a user to consume abstract storage resources
```
 kubectl create -f jenkins-pvc.yaml
 ```
6.Create a service yaml and deploy it. For accessing the Jenkins container from outside world, we should create a service and map it to the deployment.
```
 kubectl create -f jenkins-service.yaml --namespace=tools
```
7.Access the Jenkins application
```
 http://<node-ip>:port
```
Jenkins will ask for initial Admin password. You can get that from the pod logs either from kubernetes dashboard or  CLI. You can get the pod details using the following CLI command
```
 kubectl get pods --namespace=jenkins
```
And with the pod name, you can get the logs as shown below. replace the pod name with your pod name
```
 kubectl logs jenkins-deployment-2539456353-j00w5 --namespace=tools
```
The password can be found at the end of the log





