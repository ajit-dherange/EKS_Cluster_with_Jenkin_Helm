##Setup EKS MGMT Server 

###Install kubectl 
	curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
	chmod +x ./kubectl
	mv ./kubectl /usr/local/bin
	kubectl version --short --client
	
###Install AWS CLI
	Go to AWS docs for EKS cluster and from pre-requisite copy command to install latest AWS CLI
	curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
	unzip awscliv2.zip
	./aws/install  (or ./aws/install --update)
	aws --version (or /usr/local/bin/aws --version)
	
###Install eksctl 
	curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
	mv /tmp/eksctl /usr/local/bin
	eksctl version
