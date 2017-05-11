# Kubernetes-Cryptocurrency-Mining

Work in progress, yet to put up dockerfiles for images, YAML for cluster, domain of cluster dashboard

Please also note that this project was not meant for profitability, this was to learn and develop my AWS, Docker and Kubernetes knowledge.

NOTE: This readme will look raw, lots of work went into getting this working properly. Will clean up documentation as time permits, writing down raw notes for reference purposes.

Current Progress:
- Dockerfile is located in docker-template/Dockerfile. Image is pushed to Docker Hub.
- New Dockerfile replacing old one mines Zcash instead of Ethereum
- Cluster Deployed on AWS with 2 t2.micro nodes each running one container. Will beef up later and move to spot instances to get on c4.large (exciting)

My Setup:
- Vagrant box with Kops provisioned on it
	- AWS Configured for my account
- To create cluster: kops create cluster --name=MyKubernetesDomain --state=s3://MyAWSS3Bucket --zones=us-east-1c --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=MyKubernetesDomain
	- Have to confirm yes and run the update commands with the --state flag
- To Deploy App:
	- Get my zcashminer-deployment.yml
	- Run kubectl create namespace zcashminer
	- Run kubectl create -f zcashminer-deployment.yml
- To get status:
	- Run kubectl exec --namespace=zcashminer CONTAINERNAME zcash-cli getinfo
	- Other useful commands found in https://hub.docker.com/r/vjeeva/zcashminer/
