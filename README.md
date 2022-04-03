## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(ELK-Stack-Project/Images/ELK Network Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting Denial of Service (DoS) attacks to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system files.
- Filebeat collects logs about the system
- Metricbeat allows system health to be measured

The configuration details of each machine may be found below:

| Name               | Function   | IP Address | Operating System |
|--------------------|------------|------------|------------------|
| JumpBoxProvisioner | Gateway    | 10.0.0.4   | Linux            |
| Web-1              | Web Server | 10.0.0.5   | Linux            |
| Web-2              | Web Server | 10.0.0.6   | Linux            |
| Web-3              | Web Server | 10.0.0.7   | Linux            |
| ELK-Server         | Monitoring | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- 98.184.232.31

Machines within the network can only be accessed by the Jump Box Provisioner.
- The private IP address of the Jump Box Provisioner is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses           |
|--------------------|---------------------|--------------------------------|
| JumpBoxProvisioner | Yes                 | 98.184.232.31 (SSH Port 22)    |
| Web-1              | No                  | 98.184.232.31 (HTTP Port 80)   |
| Web-2              | No                  | 98.184.232.31 (HTTP Port 80)   |
| Web-3              | No                  | 98.184.232.31 (HTTP Port 80)   |
| ELK-Server         | No                  | 98.184.232.31 (HTTP Port 5601) |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because these configurations can be infinitely scalable and easily deployed to new virtual machines.

The playbook implements the following tasks:
- Install Docker
- Increase VM memory allocation
- Download and launch ELK Docker container
- Enable Docker service upon boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(ELK-Stack-Project/Images/Docker-PS.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.5
- Web-2: 10.0.0.6
- Web-3: 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to monitor file system logs across a wide array of devices. These logs can be useful to monitor suspcious activity
- Metricbeat gives us device health information, such as uptime or information about resource intensive processes 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file to the Ansible container.
- Update the configuration file to include the ELK server's IP address
- Run the playbook, and navigate to http://[ELK.server.ip]:5601/app/kibana to check that the installation worked as expected.


- Which file is the playbook?
	- filebeat-playbook.yml
- Where do you copy it?
	- Copy the playbook to /etc/ansible/files
- Which file do you update to make Ansible run the playbook on a specific machine?
	- /etc/ansible/hosts
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
	- I recommend creating 'ELK' and 'Webservers' groups in the /etc/ansible/hosts file 	to allow for easier management
- Which URL do you navigate to in order to check that the ELK server is running?
	- http://[ELK.server.ip]:5601/app/kibana
	- In my case, it is http://23.99.89.2:5601/app/kibana#, but your IP will be different
	
!(ELK-Stack-Project/Images/ELK_SystemLogs_Kibana.png)	
	
