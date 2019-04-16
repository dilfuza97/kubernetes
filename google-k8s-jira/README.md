# Jira
  Jira is a proprietary issue tracking product developed by Atlassian that allows bug tracking and agile project management. 
  Jira is a family of products built to help all types of teams manage their work. Jira offersseveral products and deployment options that are purpose-built forSoftware, IT, Business, Ops teams, and more. Read on to see which is right for you.
   Products and apps built on top of the Jira platform help teams plan, assign, track, report and manage work. The Jira platform brings teams together for everything from agile software development and customer support to managing shopping lists and family chores.
Four products are built on the Jira platform: Jira Software, Jira Service Desk, Jira Ops, and Jira Core. Each product comes with built-in templates for different use cases and integrates seamlessly, so teams across organizations can work better together.


To create Jira deployment follow, this steps.

Create the namespace.
```
kubectl create -f namespace.yml
```
 
Next command will create pvc,  it’s  will make dada persistent. In case if pod goes down, dada will be stable.

```
kubectl create -f pvc_jira.yml -n tools
``` 

Next  command will create actual deployment, mount it to pvc created earlier. Also you have option to specify, how mach resource do you want to give. 
```
kubectl create -f jira.yml -n tools
```

The next step will be create the service Jira, which will expose actually deployment over load balancer. 
```
kubectl create -f service-jira.yml -n tools
```

To check if it works, copy IP address and specify target port over url.

