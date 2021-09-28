## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Image of Network Diagram](https://github.com/ahong117/UCI-Project1/blob/31892db63adca7d90b65b41da8ba5cabb156433b/Images/network_diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration file may be used to install only certain pieces of it, such as Filebeat.

 
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box? A load balancer protects the availability of a webserver by distributing traffic so that it is hard to perform DDOS attacks.  An advantage of using a jumpbox is making a secure computer to have everybody connect to first before accessing our webservers.  

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
What does Filebeat watch for? Filebeat watches out for changes to system logs 
What does Metricbeat record? Metricbeat records information as metric data for certain services such as Redis, MySQL, Apache...etc

The configuration details of each machine may be found below.


| Name        | Function     | IP address | Operating System |
|-------------|--------------|------------|------------------|
| Jumpbox     | Gateway      | 10.0.0.1   | Linux            |
| Webserver 1 | Collect Data | 10.0.0.2   | Linux            |
| Webserver 2 | Collect Data | 10.0.0.3   | Linux            |
| ELK Stack   | Monitor WS   | 10.0.0.4   | Ubuntu           |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- I configured my jumpbox so that anybody could access it 

Machines within the network can only be accessed by: 
The only machine that should be able to access the ELK VM should be the Jumpbox VM and its private IP address is 172.31.0.18

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-The main advantage of configuration with ansible is that it is free and very easy to use and set up a playbook to do whatever we want like creating a webserver

This the ELK configuration file that I ran on my ansible container
[install-elk.yml Link](https://github.com/ahong117/UCI-Project1/blob/0b08a98000ae430c9a4e5d6e069ecf32770b5854/Ansible/install-elk.yml)

The playbook implements the following tasks:
- Install Docker.io on the Ubuntu VM that we created to be our ELK stack
- Install python3-pip
- Install our Docker python module
- Download and launch our docker web container with the image sebp/elk:761 and allow ports 9200, 5601, 5044 open. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Image of Docker ps](https://github.com/ahong117/UCI-Project1/blob/1881d4c16836066f53c4a3b1d4e17353d72b959d/Images/docker_ps_output.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-172.31.10.189
-172.31.88.184

We have installed the following Beats on these machines:
-Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat collects data on system logs such as server logs or audit logs.  Metricbeat collects statistical data and metrics on our Apache server and any services running on that server.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to ansible container.
- Update the hosts file to include the IP addresses of the 2 webservers as a group and the IP address of the ELK stack under a group called elk
- Run the playbook, and navigate to the ELK stacks public IP address and access it through port 5601 to see if our ELK server is running. 

