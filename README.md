## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Elk Stack](https://github.com/Jtullis316/Elk-Stack/blob/main/Images/Elk%20Stack%20diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - [Install Elk playbook](https://github.com/Jtullis316/Elk-Stack/blob/main/Playbooks/Install-Elk.yml)
  - [Filebeat Playbook](https://github.com/Jtullis316/Elk-Stack/blob/main/Playbooks/Filebeat.yml)
  - [Metricbeat Playbook](https://github.com/Jtullis316/Elk-Stack/blob/main/Playbooks/Metricbeat.yml)
  - [The first Playbook](https://github.com/Jtullis316/Elk-Stack/blob/main/Playbooks/My-playbook.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- The aspect of security the load balancers protect againsts is the DDOS attacks. The advantage of a jump box is the starting point before you can start your tasks. You will have to start the jumpbox before you start or do any tasks first.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat watches log files from the virtual machines and used to collect files as from specific files.
- Metricbeat records the metrics from the operating system and from services that are running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| Elk      | Server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- (Your personal IP address for your personal computer)

Machines within the network can only be accessed logging in from the jumpbox machine via ssh.
- The Jumpbox allows you access to your ELK VM and the address is  IP address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses     |
|----------|---------------------|--------------------------|
| Jump Box | Yes                 |     Public IP Address    |
| Web-1    | No                  |     10.0.0.4             |
| Web-2    | No                  |     10.0.0.4             |
| Elk      | Yes                 |Public IP Address,10.0.0.4|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantage of automating configuration with Ansible is that it can work on multiple machines at the same time after you run the playbooks. 

The playbook implements the following tasks:
- Install docker.io
- Install python3.pip
- Install Docker module
- Increase and use more virtual memory
- Download and launch docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://github.com/Jtullis316/Elk-Stack/blob/main/Images/Docker%20ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5 
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat  
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects data from log events and ships them, an example is Winlogbeat that ships windows event logs. Metricbeat collects metric data from servers and ships them. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config and metricbeat-config files to /etc/ansible/files directory.
- Update the config files to add the Elk Stack server's private IP address to "output.elasticsearch" "hosts" section and to "setup.kibana" "host" section
- Update the hosts in the /etc/ansible/hosts file. Add the ip address of web-1 and web-2 to the "webservers" and create "Elk" under the ip addresses and put the ip address of the elk server under it.
- Run the playbook, and navigate to the Elk virtual machine to check that the installation worked as expected.
- Filebeat.yml and Metricbeat.yml are the files that are the playbooks. You copy them to the /etc/ansible/roles directory.
- You update the hosts file whicle usually can be found in /etc/ansible/hosts to make Ansible run the playbook on a specific machine. To specify which machine you're going to host the Elk server on, you are going to go into the hosts file and create "elk" and put the elk ip address under it. You will then have edit the elk playbook file and make sure for "hosts" its elk. To install Filebeat you would change the hosts in the playbook to webservers.
- In order to check that the ELK server is running, you will go to the url http://[your Elk VM IP address]:5601/app/kibana

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
- ssh *your administration username*@jumpbox private ip address
- sudo docker container list -a
- sudo docker container start *containter name*
- sudo docker container attach *container name*
- sudo ansible-playbook playbook.yml
