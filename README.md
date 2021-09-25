## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Image of Network Diagram](https://github.com/ahong117/UCI-Project1/blob/31892db63adca7d90b65b41da8ba5cabb156433b/Images/network_diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration file may be used to install only certain pieces of it, such as Filebeat.

  - ---
  - name: install elk
    hosts: elk
    remote_user: ubuntu
    become: true
    tasks:
    - name: docker.io
      apt:
        name: docker.io
        state: present

    - name: Increase virtual memory
      command: sysctl -w vm.max_map_count=262144



    - name: Install pip
      apt:
        name: python3-pip
        state: present

    - name: Install Docker python module
      pip:
        name: docker
        state: present

    - name: download and launch a docker web container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        published_ports:
         - "5601:5601"
         - "9200:9200"
         - "5044:5044"

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
- _TODO: What does Filebeat watch for? Filebeat watches out for changes to system logs 
- _TODO: What does Metricbeat record? Metricbeat records information as metric data for certain services such as Redis, MySQL, Apache...etc

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

Machines within the network can only be accessed by _____.
-Which machine did you allow to access your ELK VM? What was its IP address?_
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

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- First we needed to install Docker.io on the Ubuntu VM that we created to be our ELK stack
- Next we had to install python3-pip
- Next we had to install our Docker python module
- Last we had to download and launch our docker web container with the image sebp/elk:761 and allow ports 9200, 5601, 5044 open. 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-172.31.10.189
-172.31.88.184

We have installed the following Beats on these machines:
-Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
-In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects data on system logs such as server logs or audit logs.  Metricbeat collects statistical data and metrics on our Apache server and any services running on that server.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the key file to ansible container.
- Update the hosts file to include the IP addresses of the 2 webservers as a group and the IP address of the ELK stack under a group called elk
- Run the playbook, and navigate to ELK stack to check that the installation worked as expected.

 Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? We have to update the host file to specify what playbook ansible should run on which machine.  To specify which machine we wanted to install ELK server on we need to change the host file compared to if we wanted to change where we download filebeat we need to specify that in the filebeat configuration file
- _Which URL do you navigate to in order to check that the ELK server is running? We would navigate to the ELK stacks public IP address and access it through port 5601. 

