## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[NETWORK DIAGRAM](https://github.com/coppiper/Azure/blob/cd9482c0907252c97e193dd9da0ed471fb7fde0a/Diagrams/Project%20Cloud%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above.
Alternatively, select portions of the etc/ansible file may be used to install only certain pieces of it, such as Filebeat.

[FILEBEAT PLAYBOOK](https://github.com/coppiper/Azure/blob/2f9c7954a6133e278a1a05bedad5fc7efbf3ba6a/Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topologu 
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.

- 	Load balancers distribute incoming network traffic between different machines to ensure that no single machine is receiving so much traffic the network fails.  
	The advantage of using a jump box is so one hardened machine stands between the main network, minimizing the risk to the network.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system traffic patterns.

- 	Filebeat monitors the file system of the virtual machines it is installed on and records information such as what and when files have changed.
- 	Metricbeat records a variety of data such as users from what country visited the site, what time of day they visited, what they did while there
	(i.e. downloaded a file), and it also records the amount of data a particular visitor used while there.

The configuration details of each machine may be found below.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.4   | Linux            |
| Web-1    | Webserver | 10.0.0.5   | Linux            |
| Web-2    | Webserver | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.94.235.76

Machines within the network can only be accessed by the jump box provisioner.
- The jump box provisioner, with a Subnet IP Address od 10.0.0.4, is the only machine with access to the elk-stack VM via SSH on port 	22.

A summary of the access policies in place can be found in the table below.

| Name     | Pubically Accessible | Allowed IP Addresses |
|----------|----------------------|----------------------|
| Jump Box | No                   | 73.94.235.76         |
| Web-1    | No                   | 10.0.0.4             |
| Web-2    | No                   | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it provides consistent deployment and configuration across all virtual machines.  

The playbook implements the following tasks:
- Install Docker.IO
- Install pip3
- Install Docker python module
- Use more memory
- download and launch a docker elk container
- Enable service on docker boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker PS Output](https://github.com/coppiper/Azure/blob/dcfef234559ff8c61738bf056ebfc56b66db860c/Pictures/docker%20ps%20output.png)  

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5 
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors log files on the virtual machines you configured, recording things such as audit logs and server logs.  Filebeat 
  can monitor things like system.memory.free that records a running total of how much memory the virtual machine has free and a set interval.  

- Metricbeat is used to gather information such as at what time and from what country a vistor was present, what files they may have  	downloaded and the amount of netowrk bandwith they used.   

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.playbook.yml file to etc/ansible
- Update the hosts file to include [webservers] 10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- Run the playbook, and navigate to kibana dashboard to check that the installation worked as expected.

### Running the Playbook
- From the command line, enter : ansible-playbook filebeat-playbook.yml.  This will download and install filebeat, configure the system module,
  then setup, start and enable upon boot filebeat.  
