# Orchestrating-Containers-Across-Multiple-Virtual-Servers-with-Kubernetes-1

SETTING UP A KUBERNETES CLUSTER FROM GROUND UP (THE HARD WAY)

In this project, a Kubernetes cluster is manually setup from the scratch without any automated helpers in order to better understand each aspect of spinning up a Kubernetes cluster as each components are manually installed from scratch..

## STEP 1:
The first step i took was to install minikube on my local machine. This open-source tool has docker runtime pre-install on it.Using 'brew intall kminikube' installed minikube and its various dependencies which included command line interface for kubernetes callled kubectl.

### images/minikube installation.jpeg 

## STEP 2:
Install CFSSL and CFSSLJSON
The cfssl is an open source tool by Cloudflare used to setup a Public Key Infrastructure(PKI) for generating, signing and bundling TLS certificates.

## STEP 3:
Configuring Network Structure
Creating a directory named k8s-cluster-from-ground-up and changing directory: mkdir k8s-cluster-from-ground-up && cd       k8s-cluster-from-ground-up

Creating a VPC and storing its ID as a variable:

$ VPC_ID=$(aws ec2 create-vpc \
--cidr-block 172.31.0.0/16 \
--output text --query 'Vpc.VpcId'
)

Tagging the VPC so that it is named:

$ NAME=k8s-cluster-from-ground-up

$ aws ec2 create-tags \
  --resources ${VPC_ID} \
  --tags Key=Name,Value=${NAME}

Enabling DNS support for the VPC:

$ aws ec2 modify-vpc-attribute \
--vpc-id ${VPC_ID} \
--enable-dns-support '{"Value": true}'
Enabling DNS support for hostnames:
$ aws ec2 modify-vpc-attribute \
--vpc-id ${VPC_ID} \
--enable-dns-hostnames '{"Value": true}'

Setting the required region:$ AWS_REGION=eu-central-1

Configuring DHCP Options Set:

$ DHCP_OPTION_SET_ID=$(aws ec2 create-dhcp-options \
  --dhcp-configuration \
    "Key=domain-name,Values=$AWS_REGION.compute.internal" \
    "Key=domain-name-servers,Values=AmazonProvidedDNS" \
  --output text --query 'DhcpOptions.DhcpOptionsId')
Tagging the DHCP Option set:

$ aws ec2 create-tags \

  --resources ${DHCP_OPTION_SET_ID} \
  --tags Key=Name,Value=${NAME}
Associating the DHCP Option set with the VPC:
$ aws ec2 associate-dhcp-options \
  --dhcp-options-id ${DHCP_OPTION_SET_ID} \
  --vpc-id ${VPC_ID}

  ### images/network config.jpeg


