# Kubernetes-Cryptocurrency-Mining

# Introduction
The aim of this project is to have a Kubernetes cluster maintaining Cryptocurrency Mining Containers automatically. This project was not meant for profitability, this was to improve my AWS, Docker and Kubernetes knowledge.

NOTE: This readme will look raw, lots of work went into getting this working properly. Will clean up documentation as time permits, writing down raw notes for reference purposes.

# Resources and Prerequisites

ZCashMiner Docker Image: https://hub.docker.com/r/vjeeva/zcashminer/

To run local Vagrant Kops Box:
- Install Vagrant: https://www.vagrantup.com/downloads.html
- Have your terminal in the __kops-vagrant-box__ folder and run `vagrant up`.

# Architecture
NOTE: This can change! Plans for upgrades are in section __Plans and Upgrades__.

### Local

Kops Vagrant Box configured to AWS to create and maintain Kubernetes cluster on AWS.

### AWS
Zone: US East (North Virginia)
Node Size: t2.micro
Number of Nodes: 2
Master Node Size: t2.micro
Domain: To be released!

# How to Deploy
To create Kubernetes cluster on AWS with the Kops Vagrant Box:

    kops create cluster --name=MyKubernetesDomain --state=s3://MyAWSS3Bucket --zones=us-east-1c --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=MyKubernetesDomain

Note that once this runs, to complete you must any further commands with the --state=s3://MyAWSS3Bucket.

To deploy the app, first copy the __zcashminer-deployment.yml__ to your Kops Vagrant Box. Then run:

    kubectl create namespace zcashminer
	kubectl create -f zcashminer-deployment.yml
	
# Useful Commands

### Commands to operate on containers

Status:

    kubectl exec --namespace=zcashminer CONTAINERNAME zcash-cli getinfo

Generate z-address for tranfer:

    kubectl exec --namespace=zcashminer CONTAINERNAME zcash-cli z_getnewaddress
	
Generate z-addresses in wallet:

    kubectl exec --namespace=zcashminer CONTAINERNAME zcash-cli z_listaddresses

Get balances:

    docker exec CONTAINERID zcash-cli z_getnewaddress ${ADDRESS}
	
# Current Accomplishments
A list of milestones and accomplishments:
- Dockerfile is located in docker-template/Dockerfile. Image is pushed to Docker Hub.
- New Dockerfile replacing old one mines Zcash instead of Ethereum, Ethereum miner literally mined 0 hashes.
- Cluster Deployed on AWS with 2 t2.micro nodes each running one container.

# Plans and Upgrades

- Will beef up later and move to spot instances to get on c4.large (exciting)
- Kubernetes Dashboard on public domain (associated with my personal domain)
