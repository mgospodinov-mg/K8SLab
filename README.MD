# K8SLab
This project aims to facilitate the creation of simple Kubernetes cluster in AWS for learning purposes. Create the cluster as needed and subsequently destroy it. This allows you to avoid incurring costs for cloud resources during periods when the cluster is not in use. 


## Prerequisite
You should have AWS account created. If you haven't already, install and configure the AWS CLI.
OpenToFu and Ansible are also required.

## How to create simple K8S lab
Clone the repository 

```
git clone https://github.com/mgospodinov-mg/K8SLab.git
```

### Generare SSH key

Generate SSH key and put it in the "<path>/opentofu_k8slab/sshkeys" directory

```
ssh-keygen -t ed25519 -C "<comment>"
```
Note: ED25519 keys are considered more secure and performant than RSA keys.
They are compact, fast to generate, and offer better security with faster performance compared to DSA or ECDSA.

### Run OpenTofu 

By default the aws region is "us-west-2" and the instance type is "t2.large". Of course you may change them when you run the tofu command.

```
tofu plan
tofu apply
```
If you want to modify the variables

```
tofu apply -var='aws_region="us-east-1"' -var="instance_type=t2.medium"
```

### Run Ansible

In the Ansible invetory file add the public IP addresses of the master node and worker node. No need to change anything else.
Switch to the ansible directory "<path>/ansible_k8slab" and run the command

```
ansible-playbook -i inventory.ini playbooks/k8slab-playbook.yaml -v
```

### Connect to the Kuberntes cluster

Connect to the control plane using ssh. Go to the <path>/opentofu_k8slab/sshkeys directory

```
ssh -i <sshkey> ubuntu@<control plane public ip>
```

```
kubectl get nodes
```

Note: There is kubectl autocomplete installed and configured. 

