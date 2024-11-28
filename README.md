# Ansible EC2 Instance Management Tutorial

## Overview
This project is a tutorial designed to provide hands-on exposure to Ansible by managing AWS EC2 instances. It specifically demonstrates how to provision and stop EC2 instances using Ansible installed on WSL Ubuntu running on a Windows machine.

## Prerequisites
- A Windows machine with WSL Ubuntu installed.
- An AWS account with an IAM user to provision and manage EC2 instances.

## Setup Instructions

1. Install Required Software
Ensure the following software is installed in your WSL Ubuntu environment:
- **Python**: Version 3.12.3
- **pip**: Version 24.0
- **Ansible**: Version 11.0.0
- **boto3**: Version 1.35.71

Install these using the following commands:

```bash
sudo apt update
sudo apt install python3-pip
pip3 install ansible==11.0.0 boto3==1.35.71
```


2. Install the Amazon AWS Collection

Install the necessary Ansible collection to manage AWS resources:
```
ansible-galaxy collection install amazon.aws
```
3. AWS IAM User and Key Pair

Create an IAM user in your AWS account with permissions to manage EC2 instances.
Generate a key pair for password-less authentication to the EC2 instances.

4. Create and Secure AWS Access Keys

Generate an access key and secret key for your IAM user.
Use ansible-vault to securely store these keys for safe access within your playbooks.
```
openssl rand -base64 2048 > vault.pass
ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
```

5. Configure AWS Security Group

Add an inbound rule in your AWS security group to accept SSH traffic from your WSL Ubuntu machine, enabling the transfer of the .pem file for password-less authentication.

6. Ansible Playbook for EC2 Instance Management

Create an Ansible playbook utilizing the amazon.aws collection to launch and stop EC2 instances. This playbook demonstrates the use of modules, collections, loops, and when conditions.
```
ansible-playbook ec2_create.yaml --vault-password-file vault.pass
ansible-playbook -i inventory.ini ec2_stop.yaml --vault-password-file vault.pass
```
