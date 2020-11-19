# Ansible playbooks for deployment Akraino Network Cloud with Tungsten+Fabric 
===

Requirements:
  * Ubuntu 18.04
  * ansible 2.5.1
  * python3
  * boto (2.49.0)
  * boto3 (1.4.2)
  * botocore (1.8.48)

AWS authorization must be setup on the host. (check aws credentials in ~/.aws/credentials)

File  ~/.boto must contain:
~~~
[Boto]
use_endpoint_heuristics = True
~~~
  



### Creating keypair, security group and AWS EC2 spot instances and updating inventory and group_vars/all
~~~
cd akraino-ansible
ansible-playbook 00-create-environment.yaml
~~~

After this step 2 AWS instance are created and available by ssh with the identity *akraino-aws-private-key.pem*
Files inventory/akraino and group_vars/all are updated with correct ip addresses. 

### deploying Regional Controller with TF blueprint
~~~
ansible-playbook -i inventory/akraino 02-deploy-tf-blueprint.yaml
~~~

After this step Regional controller is available by https. You can see ip address of RC in file inventory/akraino or group_vars/all.
Also you can login on Regional COntroller by ssh with the command ssh -i akraino-aws-private-key.pem ubuntu@<ip_address>

TF yamls are generated and EdgeSite, Blueptint and POD are created on Regional Controller.
Process of deployment usually takes 5-6 hours.



### Cleanup the environment
~~~
ansible-playbook -i inventory/akraino akraino-playbook-cleanup.yaml
~~~
