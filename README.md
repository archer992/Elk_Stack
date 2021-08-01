# Elk_Stack Deployment
# Class project, elk stack

The files in this repository were used to configure the network depicted below.

Images/Diagram Elk_Stack.png
![image](https://user-images.githubusercontent.com/65125381/127758013-39bfb513-f9d8-4b35-becf-af48fa65b7ae.png)


These files have been tested and used to generatte a live Elk deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

Images/Pentest.yml.png


Images/install-elk.yml.png


Images/metricbeat-playbook.yml.png


Images/filebeat-playbook.yml.png


This document contains the following details:
- Description of the Topology
- Access Policies
- Elk Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

the main purpose of this Network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Applicaiton. 

Load balancing ensures that the application will be highly reliable, in addition to restricting access to the network.
- What aspect of security do load balancers protect?
Load balancers defend against distributed denial of service (DDoS) attacks. It does this by distributing traffic evenly across more than one Virtual Machine
- What is the advantage of a jump box?
The Jump box acts as a gateway to the other Virtual Machines, it also adds an extra layer of security. An advantage of a jump box is the ability to run ansible and configure other Virtual Machines in the network.

Integrating an Elk server allows users to easily monitor the vulnerable VMs for changes to the network and system files. 
- What does Filebeat watch for?
Filebeat watches for which files have been changed and when. Filebeat then logs that information and sends it Logstash and Elasticsearch.
- What does Metricbeat record?
Metricbeat records the metrics of the system and helps monitor the servers.

The configuration details of each machine may be found below.
Note: Use the [Markdown Table Generator] to add/remove values from the table.

| Name                     |          Function          | IP Address | Operating System     |
|--------------------------|:--------------------------:|:----------:|----------------------|
| Jump Box                 |          Gateway           |  10.0.0.4  | Linux (Ubuntu 18.04) |
| Web-1                    |         Web Server         |  10.0.0.5  | Linux (Ubuntu 18.04) |
| Web-2                    |         Web Server         |  10.0.0.6  | Linux (Ubuntu 18.04) |
| Web-3                    |         Web Server         |  10.0.0.7  | Linux (Ubuntu 18.04) |
| VEE-EMM1 (Elk Container) | Monitoring Web Servers 1-3 |  10.1.0.4  | Linux (Ubuntu 18.04) |


### Access Policies

The Machines on the internal network are not exposed to the public Internet.

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
76.169.110.182

Machines within the network can only be accessed by ssh through the Jump Box.
The Jump Box was the only machine allowed to access the ELK VM via SSh using its internal private IP address of 10.0.0.4 the Jump Box Vm was able to SSH into Elks VMs internal IP address of 10.1.0.4.

A summary of the access policies in place can be found in the table below.

|          Name            | Publicly Accessible |     Allowed IP Addresses     |
|:------------------------:|:-------------------:|:----------------------------:|
|        Jump Box          |         Yes         |        76.169.110.182        |
|          Web-1           |         No          |  10.0.0.4 (Internal IP Only) |
|          Web-2           |         No          |  10.0.0.4 (Internal IP Only) |
|          Web-3           |         No          |  10.0.0.4 (Internal IP Only) |
| VEE-EMM1 (Elk Container) |         No          |  10.0.0.4 (Internal IP Only) |


### Elk Configuration

Ansible was used to automate configuration of the Elk machine. No configuration was performed manually, which is advantageous because:
Using Ansible speeds up the process. I was able to save a lot of time by automating the configuration of my Virtual Machines.

The playbook implements the following tasks:
- apt module was used to install docker.io & python3-pip.
- pip module (which defualts to pip3) was used to install Docker module.
- command module was used to increase virtual memory.
- docker_container module was used to download and launch a docker elk container.

The following screenshot displays the result of running 'docker ps' after successfully configuring the Elk instance.

(Images/sudo docker ps.png)

### Target Machines & Beats
This ELK Server is configured to monitor the following machines:
Web-1: 10.0.0.5
Web-2: 10.0.0.6
Web-3: 10.0.0.7

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machines:
Filebeat collects logfile data. It is expected to see an output of this data, that output helps us monitor any changes within the log file. 
Metricbeat collects metric data. It is expectrd measure runtime, errors messages, etc..

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the 'pentest.yml file to Ansible.
- Update the 'hosts' file to include the Elk servers IP address (10.1.0.4) under ther [Elk] section. Webservers can be added under [webservers] section.
- Run the playbook, and navigate to (the Elk servers public Ip):5601/app/kibana to check that the installation worked as expected. 
