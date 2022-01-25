# DeVOps CICD

##  Project Overview
- DevOps project in which Continuous Integration/Continuous Deployment (CI/CD).
- The project makes use DevOps tools:
	- GitHub and git (Continuous Development)
	- Jenkins (continuous integration and orchestration tool)
	- Ansible (configuration management, Continuous Deployment)
	- Docker (Continuous Deployment)
	- Grafana (Continuous Monitoring tbd)
	- Terraform (Infrustructure as Code) 
- Continous testing was limited to success of the testing docker container build and website exposure.
- Continuous monitoring are considered next steps. 


## Repositories

The project makes use of the following three repositories:
- https://github.com/radleap/DevOpsProject1Ansible.git
	- Container Jenkinsfile, ansible playbooks and host files
	- Needs prod and testing host IPV4 IPs, and associated key(s)
- https://github.com/radleap/DevOpsProject1Dockerfile.git
	- Container Dockerfile for container image and index.html
	- Emulates the "app" deployed
- https://github.com/radleap/DevOpsProject1Terraform.git
	- Code requires an AWS account
	- Terraform code requires AWS access key, secret and region passed
	- Procures two EC2 instances (test and prod)
- Jenkinsfile -> executes Ansible commands..

## General Notes:
- An ubuntu 18.04 VM was used as a master node.
- Jenkins, Ansible, Terraform, Docker, and all necessisary dependencies were installed. 
- Testing and development was done on this machine. 
- When executing the terraform stage of procurement, this was manually executed prior to the Jenkins pipeline, and the resulting public IPV4s were used in the ansible playbooks and inventory files.  

## Jenkins Configuration Notes:
- Plugins:
	- plugins for Ansible, Docker, Pipleines, etc were installed.
- Credentials:
	- AWS credentials: in order to ssh into the EC2 instances, the rsa key was set in credentials (this is called in the ansible playbook as 'private-key')
	- Git repository is public otherwise credential set here
	- Dockerhub credentials were set (for projects in which dockerhub image workflow was used)
- Global Tool configuration:
	- Ansible: providing the ansible name and location /usr/bin/
	- Git 

## General Sequence of Running
- Terraform IaC procurment
- Provide EC2 public IPV4, .pem, and security group access.
- "Developers" edit the "app", our simple index.html, and push code to GitHub
- This developer repo triggers the Jenkins pipeline
- Jenkins pipeline pulls the developer (Dockerfile + index.html)
- Jenkins uses the EC2 test instance, installs docker, builds image, and deploys on the test server EC2 instance.
- If not a failure (basically our test here), Jenkins kicks of the same on the production EC2 instance. 
- Ultimate output is the website, if passes tests, is successfully deployed to internet. 
