## Abiquo 3.2 KVM Server node playbook

- Requires Ansible 1.4 or newer
- Expects CentOS/RHEL 6.x hosts
- Access via ssh key to hosts
- You may need to give access through ssh and setup selinux and iptables accordingly

Edit the "hosts" inventory file and specify the hostnames or ip address of the machines
on which you want to deploy Abiquo Server and edit the group_vars/abiquo-kvm file to 
set any configuration parameters you need.

To install an Abiquo 3.2 KVM server node simply run:

	ansible-playbook -i hosts abiquo-kvm.yml


These are some of the optional --extra-vars you can specify to abiquo.yml playbook.
You can check all existing --extra-vars and change default value by editing group_vars/abiquo-kvm file.

When the playbook run completes, you should have an Abiquo KVM server node ready to use with Abiquo.

We would love to see contributions and improvements, so please fork this
repository on GitHub and send us your changes via pull requests.