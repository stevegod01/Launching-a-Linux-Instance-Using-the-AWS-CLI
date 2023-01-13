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
