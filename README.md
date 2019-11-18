# Ansible playbooks for deployment Akraino Network Cloud with Tungsten+Fabric 
===

Requirements:
  ansible >= 2.5.1
  python3
  boto (2.49.0)
  boto3 (1.4.2)
  botocore (1.8.48)

aws credentials in ~/.aws/credentials

File  ~/.boto should contain:
~~~
[Boto]
use_endpoint_heuristics = True
~~~
  



### deploying keypair, security group and AWS EC2 spot instance and updating inventory and group_vars/all
~~~
ansible-playbook -i inventory/akraino akraino-playbook-step01.yaml
~~~

### deploying Regional Controller and starting airship-in-a-bootle deployment
~~~
ansible-playbook -i inventory/akraino akraino-playbook-step02.yaml
~~~

### Cleanup the environment
~~~
ansible-playbook -i inventory/akraino akraino-playbook-cleanup.yaml
~~~
