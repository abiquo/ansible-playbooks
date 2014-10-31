## Abiquo Monitoring node deployment playbook

- Requires Anisble 1.6 or higher
- Expects CentOS 6.x hosts
- Cassandra requires a host with at least 2GB RAM
- This playbook is intended to run locally
- This playbook installs latest Cassandra version
- This playbook installs KairosDB v 0.9.4

Install required packages:
```
	rpm -Uvh http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
	yum install -y ansible libselinux-python git-core
```

Download and unzip OR git clone Abiquo anible-playbooks git repository:
```
	git clone https://github.com/abiquo/ansible-playbooks.git
```

To install an Abiquo Monitoring Server simply run:
```
	cd ansible-playbooks/abiquo-monitoring
	ansible-playbook monitoring.yml
```

That's all, you have now a Cassandra+KairosDB node running.
