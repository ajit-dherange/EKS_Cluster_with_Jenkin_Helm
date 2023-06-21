# Setup Kubernetes on Amazon EKS

You can follow same procedure in the official  AWS document [Getting started with Amazon EKS – eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)   

#### Pre-requisites: 
  - An EC2 Instance (Kubernetes Management Host)
# 
1. Install and setup kubectl on Management host
   a. Download kubectl version 1.19.6 
   b. Grant execution permissions to kubectl executable   
   c. Move kubectl onto /usr/local/bin   
   d. Test that your kubectl installation was successful    
   ```sh 
   curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
   chmod +x ./kubectl
   mv ./kubectl /usr/local/bin 
   kubectl version --short --client
   ```
2. Install and setup eksctl on Management Host   
   a. Download and extract the latest release   
   b. Move the extracted binary to /usr/local/bin   
   c. Test that your eksclt installation was successful   
   ```sh
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   sudo mv /tmp/eksctl /usr/local/bin
   eksctl version
   ```


3. Create an IAM Role and attache it to EC2 instance Management Host  
   `Note: create IAM user with programmatic access if your bootstrap system is outside of AWS`   
   IAM user should have access to   
   IAM   
   EC2   
   VPC    
   CloudFormation

## 1) Create EKS cluster using aws console

**1. Create ekscluster role:**
 
	Open the IAM console at https://console.aws.amazon.com/iam/.
	Choose Roles, then **Create role**.
	Under Trusted entity type, select AWS service.
	From the Use cases for other AWS services dropdown list, choose EKS
	Choose **EKS - Cluster** for your use case, and then choose Next.
	On the Add permissions tab, choose Next.
	For Role name, enter a unique name for your role, such as **eksClusterRole**.
	For Description, enter descriptive text such as Amazon EKS - Cluster role.
	Choose Create role.
	# Use this role while creating cluster on console
	
**2. Create EKS cluster:**
 
	Open the Amazon EKS console at https://console.aws.amazon.com/eks/home#/clusters.
	Choose **Add cluster** and then choose Create.
	On the Configure cluster page, enter the following fields:
	**Name** – A name for your cluster. It must be unique in your AWS account. The name can contain only alphanumeric characters (case-sensitive) and hyphens. It must start with an alphabetic character and can't be longer than 100 characters. The name must be unique within the AWS Region and AWS account that you're creating the cluster in.
	**Kubernetes version** – The version of Kubernetes to use for your cluster. We recommend selecting the latest version, unless you need an earlier version.
	**Cluster service role **– Choose the Amazon EKS cluster IAM role that you created to allow the Kubernetes control plane to manage AWS resources on your behalf.
	**Secrets encryption** – (Optional) Choose to enable secrets encryption of Kubernetes secrets using a KMS key. You can also enable this after you create your cluster. Before you enable this capability, make sure that you're familiar with the information in Enabling secret encryption on an existing cluster.
	**Tags** – (Optional) Add any tags to your cluster. For more information, see Tagging your Amazon EKS resources.
	Choose Next.
	On the Specify networking page, Choose Next 
	On the Configure logging page, Choose Next
	On the Select add-ons page, Choose Next
	On the Configure selected add-ons settings page, Choose Next
  	On the Review and create page, Choose Next

 
### Create EKS cluster and nodes from EC2 Management Host
   4. Create EKS cluster
   ```
   eksctl create cluster --name cluster-name  \
   --region region-name \
   --node-type instance-type \
   --nodes-min 2 \
   --nodes-max 2 \ 
   --zones <AZ-1>,<AZ-2>
   
   example:
   eksctl create cluster --name cloudfreak-cluster \
      --region ap-south-1 \
   --node-type t2.medium \
   ```
   
5. Validate your cluster using by creating by checking nodes and by creating a pod 
   ```
   kubectl get nodes
   kubectl run pod tomcat --image=tomcat 
   ```
   
   
### To delete the EKS clsuter 
   ``` 
   eksctl delete cluster cloudfreak-cluster --region ap-south-1
   ```
