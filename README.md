## Udacity Cloud DevOps Engineer Nanodegree Program - Capstone Project
### The project
This is a demonstration of an automated process for application deployment, including 
Infrastructure as Code (IAC) and a CI/CD pipeline.
This is a good way of building scaleable, fault tolerant and robust applications.   
### Infrastructure
AWS CloudFormation script is used to set up the infrastructuere in AWS, the scripts are located
in the `stack` folder

Set up the VPC and network infrasrtructure:
```bash
aws cloudformation create-stack --stack-name <your-network-stack-name> --region <your-region> --template-body file://network.yml --parameters file://params.json
```

Setting up the Kubernetes Cluster
```bash
aws cloudformation create-stack --stack-name <your-stack> --region <your-region> --template-body file://cluster.yml --parameters file://cluster-params.json --capabilities CAPABILITY_NAMED_IAM
```
### CI/CD Pipeline
The pipeline is implemented in Jenkins and the script is defined in the `Jenkinsfile`.  
Steps:  
- Linting - Linting the `Dockerfile with [Hadolint](https://github.com/hadolint/hadolint)
- Building docker image locally
- Pushing image to [dockerhub](hub.docker.com)
- Clean up - delete local image
- Deploy to kubernetes cluster (rolling deployment)

#### Rolling Deployment
Rather than updating all pods simultaneously, new pods are added before old ones are terminated, thus the transition is seamless and does not cause downtime:  
- Update initiated to update some of the pods in a kubernetes cluster  
- The new pods are rolled out  
- If the rollout is successful the old pods are terminated (otherwise they remain active)  
A rolling deployment is used to reduce application downtime and unforeseen consequences or errors in software  updates.  
The pace of rollout is configured by the following parameters:  
- `maxSurge`: The number of pods that can be created above the desired amount of pods during an update  
- `maxUnavailable`: The number of pods that can be unavailable during the update process  

See the `k8s/capstone.yml`file for reference.  

### The App
The app is a single page appliacion that was created with [vue](vuejs.org) and [vueatify](https://vuetifyjs.com).





