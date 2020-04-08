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
- Deploy to kubernetes cluster

### The App
The app is a single page appliacion that was created with [vue](vuejs.org) and [vueatify](https://vuetifyjs.com).

### URL
The deployed application can be found here:




