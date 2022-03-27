# ELK Stack Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img src="Diagrams/project_1_diagram.jpg" alt="ELK Stack Network Diagram" title="ELK Stack Network Diagram">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the ELK installation file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

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
- What aspect of security do load balancers protect?
Load balancers ensure the availability of the application by distributing traffic across multiple servers.
- What is the advantage of a jump box?
The jump box controls access to the internal virtual machines and provides security by requiring traffic to use SSH.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system metrics.
- What does Filebeat watch for?
Filebeat collects data about the file system.
- What does Metricbeat record?
Metricbeat collects machine metrics, such as uptime.

The configuration details of each machine may be found below.

| **NAME** |  **FUNCTION**  | **IP ADDRESS** | **OPERATING SYSTEM** |
|:--------:|:--------------:|:--------------:|:--------------------:|
| Jump Box |     Gateway    |    10.0.0.4    | Linux (Ubuntu 18.04) |
| Web 1 VM | DVWA Container |    10.0.0.5    | Linux (Ubuntu 18.04) |
| Web 2 VM | DVWA Container |    10.0.0.6    | Linux (Ubuntu 18.04) |
|  ELK VM  |   Log Server   |    10.1.0.4    | Linux (Ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP

Machines within the network can only be accessed by SSH. The ELK VM is accessible through the Jumpbox VM with the IP address of 10.0.0.4. 

A summary of the access policies in place can be found in the table below.

| **NAME** | **PUBLICLY ACCESSIBLE** | **ALLOWED IP ADDRESSES** |
|:--------:|:-----------------------:|:------------------------:|
| Jump Box |           Yes           |        Personal IP       |
| Web VM 1 |            No           |         10.0.0.4         |
| Web VM 2 |            No           |         10.0.0.4         |
|  ELK VM  |            No           | 10.0.0.4 and Personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because multiple machines can be configured quickly using a YAML script file and without the risk of errors that can occur when configuring machines one at a time.

The playbook implements the following tasks:

- Install docker.io, python3-pip, and the docker module
- Increase memory for virtual machines
- Download and launch docker ELK container
- Enable docker when booting machine

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

-

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web VM 1 10.0.0.5
- Web VM 2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects specific types of log files, such as those generated by Azure, MySQL, and Apache. With this information, we can identify changes that have been made to the file system.
- Metricbeat is a tool that allows us to collect and study metrics about each machine within the network. CPU usage, storage, and uptime are available modules to track system metrics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat and metricbeat configuration files to the etc/ansible/roles directory.
- Update the filebeat configuration file to include the IP address of the ELK machine.
- Run the playbook, and navigate to the Filebeat installation page on the ELK server GUI to check that the installation worked as expected.

- Which file is the playbook? Where do you copy it?
filebeat-playbook.yml copied to the /etc/ansible/roles directory.
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
Specifying which machine to install the ELK server on can be done through the header of the install-elk.yml file. Editing the filebeat-playbook file can specify on which machine to install Filebeat.
- Which URL do you navigate to in order to check that the ELK server is running?
http://[your.ELK-VM-EXTERNALIP]:5601/app/kibana
