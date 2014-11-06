## Abiquo 3.1 Server deployment playbook

- Requires Ansible 1.4 or newer
- Expects CentOS/RHEL 6.x hosts
- Access via ssh key to hosts
- You may need to give access through ssh and setup selinux and iptables accordingly

Oracle license disclaimer
	This playbook installs Oracle JDK 1.7 and Oracle JCE (Java Cryphtography Extension) 1.7
	Is up to you change jdk playbook role to install OpenJDK instead.
	If you install this playbook with default Oracle JDK and JCE versions, you are accepting
	Oracle license agreement:
	http://www.oracle.com/technetwork/es/java/javase/downloads/jdk7-downloads-1880260.html
	http://www.oracle.com/technetwork/es/java/javase/downloads/jce-7-download-432124.html

This playbook deploy an Abiquo 3.1 server.

You can deploy 4 different profiles by specifying --extra-vars when executing the playbook:

	abiquo_profile=monolithic
	abiquo_profile=api-server
	abiquo_profile=public-cloud-node
	abiquo_profile=remote-services

Edit the "hosts" inventory file and specify the hostnames or ip address of the machines
on which you want to deploy Abiquo Server and edit the group_vars/abiquo-server file to 
set any configuration parameters you need.

To install an Abiquo 3.1 Monolithic server simply run:

	ansible-playbook -i hosts abiquo.yml

Also, depending on the selected profile you would like to install, you may want to specify
some more extra-vars to get the server installed and configured at once.

These are some of the optional --extra-vars you can specify to abiquo.yml playbook:

	abiquo_self_certificate_ssl=true : Enable SSL on the Abiquo UI by creating a self-signed certificate.
	Default value: true
	Profiles: monolithic, api-server

	abiquo_rabbitmq_host=192.168.1.100 : Specify RabbitMQ server IP address.
	Default value: 127.0.0.1
	Profiles: all

	abiquo_datacenter_id=abiquo_london : Specify the Abiquo datacenter ID.
	Default value: Abiquo
	Profiles: monolithic, remote-services, 

	abiquo_abiquo_security_encrypt=true : Enables Abiquo encryption for all credentials stored in Abiquo database. 
	Default value: true
	Profiles: all

	abiquo_vsm_syncfrequency=200000 : Time in milliseconds configured for the abiquo.vsm.vmsyncfrequency.provider Abiquo property.
	Default value: 200000 milliseconds
	Profiles: monolithic, remote-services, public-cloud-node

etc.

You can check all existing --extra-vars and change default value by editing group_vars/abiquo-server file.

Examples:

This ansible run will install an Abiquo 3.1 Remote Services server with some extra parameters configured:

	ansible-playbook -i hosts abiquo.yml --extra-vars "abiquo_profile=remote-services abiquo_rabbitmq_host=80.240.136.123 abiquo_devel=true abiquo_datacenter_id=barcelona abiquo_api_url=http://80.240.136.123:8009/api"

When the playbook run completes, you should be able to see the Abiquo Server
running on the ports choosen ports in the target machines.

You may need to performe some configuration depending on your environment. Please, have a read to:

- Abiquo documentation: http://wiki.abiquo.com/display/ABI31/Abiquo+Documentation+Home
- Abiquo configuration properties: http://wiki.abiquo.com/display/ABI31/Abiquo+Configuration+Properties

We would love to see contributions and improvements, so please fork this
repository on GitHub and send us your changes via pull requests.