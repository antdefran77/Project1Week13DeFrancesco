## Elk_Stack_Project

In this project, I set up a small virtual network infrastructure and configured a cloud monitoring system via an ELK stack server.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Virtual Netwrok Security Diagram](Diagrams/azure_resource_group_elk.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

![Filebeat Playbook](Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- A load balancer protects from a Distributed Denial-of-Service (DDos) 
- What is the advantage of a jump box? A jump box is the main hub of control for other machines and controls access by allowing connections from specific IP addresses, then forwarding those connections to their respective machines

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- What does Filebeat watch for? Filebeat watches and collects data about the file system.
- What does Metricbeat record? Metricbeat records and collects operating machine metrics.

The configuration details of each machine may be found below.

| Name                 | Function      | IP Address       | Operating System |
|----------------------|---------------|------------------|------------------|
| Jump-Box-Provisioner | Gateway       | 52.186.147.254   | Linux            |
| Web-1                | UbuntuServer  | 10.1.0.8         | Linux            |
| Web-2                | UbuntuServer  | 10.1.0.9         | Linux            |
| ElkVM                | UbuntuServer  | 10.0.0.4         | Linux            |
| RedTeamLB            | Load Balancer | 52.188.159.145   |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.30.XXX.XXX/32

Machines within the network can only be accessed by SSH.
- Which machine did you allow to access your ELK VM? Jump-Box-Provisioner
- What was its IP address? 52.186.147.254

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump-Box-Provisioner | Yes                 | 73.30.XXX.XXX/32     |
| Web-1                | No                  | 10.1.0.7             |
| Web-2                | No                  | 10.1.0.7             |
| ElkVM                | No                  | 10.1.0.7             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually.

- What is the main advantage of automating configuration with Ansible? Automating with Ansible allows you to create consistent, reproducable results throughout multiple machine configurations.

The playbook implements the following tasks:
- Explain the steps of the ELK installation play.
 - Instal docker.io
 - Instal python3.pip
 - Install docker module
 - Increase virtual memory
 - Use more memory
 - Download and lauch a docker elk container through published ports:
   - 5601:5601
   - 9200:9200
   - 5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker ps](Ansible/docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.1.0.8
- Web-2: 10.1.0.9
- ElkVM: 10.0.0.4

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat: monitors the log files or locations that you specify, such as Syslogs, Sudo commands, SSH logins, and New users and groups. This is illustrated by Kibana below:

![Filebeat Kibana](Ansible/filebeat_dash.png)

- Metricbeat: monitors the metrics and statistics of the operating system, such as CPU usage, memory usage, and docker containers. This is demonstrated by Kibana below:

![Metricbeat Kibana](Ansible/metricbeat_dash.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml file to the ansible directory.
- Update the /etc/ansible/ansible.cfg file to include...
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- Which file is the playbook? the .yml file
- Where do you copy it? /etc/ansible, /etc/ansible/files, or /etc/ansible/roles depending on the .yml   file. Filebeat and Metricbeat are stored in the /etc/ansible/roles directory.
- Which files do you update to make Ansible run the playbook on a specific machine? 
  /etc/ansible/hosts and /etc/ansible/ansible.cfg
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
  By editing the /etc/ansible/hosts file with the approriate IP addresses.
- Which URL do you navigate to in order to check that the ELK server is running?
  http://<local.host>/app/kibana#/home
As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

- nano /etc/ansible/ansible.cfg
- nano /etc/ansible/hosts
- ansible all -m ping
- nano <your-playbook.yml>
- ansible-playbook <your-playbook.yml>
- ssh ansible@<XX.X.X.X>
- curl <local.host>/setup.php
