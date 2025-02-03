##Highly Available Microservices Architecture with Consul Service Mesh on AWS EKS and Linode LKE
Creating a service mesh using HashiCorp's Consul to manage communication within a cluster of microservices (open-source microservice application from Google) and deploying it in AWS EKS using Terraform using GitHub Actions to automate this process and also connecting a replica of this application in LKE using a mesh gateways to ensure high availability, ensure zero downtime in case of service failure and load balancing.


### Demo project on consul 


Terraform commands to execute the script

```sh
# initialise project & download providers
terraform init

# preview what will be created with apply & see if any errors
terraform plan

# exeucute with preview
terraform apply -var-file terraform.tfvars

# execute without preview
terraform apply -var-file terraform.tfvars -auto-approve

# destroy everything
terraform destroy

# show resources and components from current state
terraform state list
```
#### to install and configure consul using helm
```sh
# install consul using helm
helm install aws hashicorp/consul --version 1.0.0 --value consul-values.yaml --set gobal.datacenter=aws
# vice versa for lks
```

#### Get access to EKS cluster
```sh
# install and configure awscli with access creds
aws configure

# check existing clusters list
aws eks list-clusters --region eu-central-1 --output table --query 'clusters'

# check config of specific cluster - VPC config shows whether public access enabled on cluster API endpoint
aws eks describe-cluster --region eu-central-1 --name myapp-eks-cluster --query 'cluster.resourcesVpcConfig'

# create kubeconfig file for cluster in ~/.kube
aws eks update-kubeconfig --region eu-central-1 --name myapp-eks-cluster

# test configuration
kubectl get svc
```
