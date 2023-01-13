# Launching-a-Linux-Instance-Using-the-AWS-CLI

When we purchase a laptop, we have a physical device in front of us that we can log in to after setting up our account. However, EC2 instances are in the cloud, and we are expected to connect to our instances to manage hardware, maintain software, deploy application packages, and complete other tasks.

## Objectives
1. Launch an EC2 instance using the AWS CLI
2. Create key pairs and network resources using the AWS CLI
3. Verify the instance in the AWS Console

## Create a Key Pair
We'll use the AWS CLI to create a key pair easily, without having to navigate through UI screens on the AWS Console.
```Bash
# Execute this command to get the key created and uploaded to AWS

aws ec2 create-key-pair --key-name my-lab04-keypair --key-type rsa --key-format pem --query "KeyMaterial" --output text > my-lab04-keypair.pem
echo "Key pair was successfully created"
```
Execute this command to create a new my-lab04-keypair key, or adjust the command to create a key using the name of your choice. The public key is automatically uploaded to AWS, while the private key is written to a file (my-lab04-keypair.pem) in the local directory. To check this, issue ls -latr at the command prompt—you should see the file containing our newly created key pair in the list.

## Creating a VPC
A virtual private cloud is a private network that will help segregate and construct a portion of the AWS Cloud for our purposes. All resources that we create must be present in a VPC.
```bash
echo "Creating a VPC"

VPC_ID=`aws ec2 create-vpc --cidr-block 10.0.0.0/16 --query Vpc.VpcId --output text`
echo "Successfully created a VPC: $VPC_ID"
```
## Creating a Subnet
A subnet is a logical grouping of IP addresses. We usually assign a set of IP addresses in that subnet to resources like instances.
```bash
echo "Creating a subnet"

SUBNET_ID=`aws ec2 create-subnet --vpc-id $VPC_ID --cidr-block 10.0.1.0/24 --query Subnet.SubnetId --output text` 
echo "Successfully created a subnet: $SUBNET_ID"
```
## Creating an Internet Gateway
An internet gateway permits our resources in the VPC to talk to external resources on the internet. With the following command, we'll create an internet gateway and attach it to our VPC:
```bash
echo "Configuring an internet gateway"

INTERNET_GATEWAY_ID=`aws ec2 create-internet-gateway --query InternetGateway.InternetGatewayId --output text`

echo "Successfully created an internet gateway: $INTERNET_GATEWAY_ID"
echo "Attaching this internet gateway to our VPC"

aws ec2 attach-internet-gateway --vpc-id $VPC_ID --internet-gateway-id $INTERNET_GATEWAY_ID
```
