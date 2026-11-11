# Ansible Integration in Jenkins
This project uses a Jenkins pipeline to configure 2 EC2 instances using a ansible commands executed on a control node. Basically, the Jenkins job uses ``sshagent`` to ssh into the control node. It then executes the `ansible-playbook` using the playbook defined in `ansible/my-playbook.yaml`. The ``ansible`` folder is first copied to the control node using ``scp`` to make this possible. We also use dynamic inventory here by using the aws plugin. The dynamic inventory is defined in `ansible/inventory_aws_ec2.yaml`. Note: You need EC2 instances with ``name``: ``prod_server`` in aws to be able to apply the configurations. See hosts in the plays.

The control node also needs a private ssh key for applying the configuration to the EC2 managed nodes. This private key is also copied by Jenkins to the control node using ``scp``

## The pipeline performs the following steps:
1. Copy the `ansible` directory and the private key for managed EC2 instances to the control node using ``sshagent`` and ``scp``.
2. ssh into the control node and install the ansible and the required dependencies (boto3) using `prepare-ansible-server.sh` .
3. Execute ``ansible-playbook`` command to configure the managed EC2 instances.

The ansible playbook basically install docker and docker-compose on the managed EC2 instances.
