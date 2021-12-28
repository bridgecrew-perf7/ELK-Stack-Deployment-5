# Project1_Cybersecurity
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/khadijahmoore19/Project1_Cybersecurity/blob/main/Diagrams/Network%20Topology1.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

https://github/khadijahmoore19/Project1_Cybersecurity/blob/main/Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored ins$

Load balancing ensures that the application will be highly effective, in additinal lLoad balancers help protect the network from denial of service attacks by evenl$

Integrating an ELK server allows users to easily monitor the vulnerable VMs for$
- Filebeat uses logfiles to detect changes and times of occurence in files.
- Metricbeat records metrics from running services and OS. Kibana can be used t$
The configuration details of each machine may be found below.
Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdow$

| Name     |      Function     | IP Address | Operating System |
|----------|-------------------|------------|------------------|
| Jump-Box | Gateway           | 10.0.0.7   | Linux            |
| Web-1    | Run DVWA          | 10.0.0.10  | Linux            |
| Web-2    | Run DVWA          | 10.0.0.9   | Linux            |

^G Get Help  ^O WriteOut  ^R Read File ^Y Prev Page ^K Cut Text  ^C Cur Pos
^X Exit      ^J Justify   ^W Where Is  ^V Next Page ^U UnCut Text^T To Spell
### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly effective, in addition to restricting access to the network.
Load balancers help protect the network from denial of service attacks by evenly distributing network application traffic among servers. This helps to ensure one server is not overloaded with traffic. One advantage of a jump box is the limited access it provides. The public can not connect to a VM on the network without possessing the private ip address of the Vm. They  must connect to the jump box VM first. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat uses logfiles to detect changes and times of occurence in files. 
- Metricbeat records metrics from running services and OS. Kibana can be used to view metric results.  
The configuration details of each machine may be found below.
Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     |      Function     | IP Address | Operating System |
|----------|-------------------|------------|------------------|
| Jump-Box | Gateway           | 10.0.0.7   | Linux            |
| Web-1    | Run DVWA          | 10.0.0.10  | Linux            |
| Web-2    | Run DVWA          | 10.0.0.9   | Linux            |
| ELK      | Run ELK container | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 71.90.210.60

Machines within the network can only be accessed by Jump-Box VM.
Which machine did you allow to access your ELK VM? Jump-Box VM 
What was its IP address? 20.85.225.50

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses  |
|----------|---------------------|-----------------------|
| Jump Box | Yes                 | 71.90.210.60 (my ip)  |
| Web-1    | No                  | 10.0.0.7 (Jump-Box ip)|
| Web-2    | No                  | 10.0.0.7              |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because ansible can be run from the command line without needing to use configuration files to complete simple tasks.

The playbook implements the following tasks:
- Installs docker.io on ELK VM
- Installs Python 
- Increases virtual memory to 262144
- Installs, downloads, and launches a docker elk container 
- Enables docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github:com/khadijahmoore19/Project1_Cybersecurity/blob/main/Images/docker-ps output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.0.0.10 
- Web-2: 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors, collects, and records logs that specify if and when a file has been changed. Kibana can be used to view data collected by filebeat. Metricbeat monitors processes and services running on the OS and servers including but not limited to CPU usage, memory, network and disk IO, etc. Kibana can also be used to view data collected via metricbeat. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to etc/ansible/filebeat-config.yml.
- Update the filebeat-config.yml file to include host "10.2.0.4:9200" and change setup.kibana host to "10.2.0.4:5601"
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

Common questions
- Which file is the playbook? filebeat.yml
- Where do you copy it? /etc/ansible/roles/filebeat.yml
- Which file do you update to make Ansible run the playbook on a specific machine? Filebeat-config.yml
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? The ips of the machines needing access have to be added to the hosts file. The filbeat.yml file hosts section must be edited to indicate installation location (Elk or webservers)
- Which URL do you navigate to in order to check that the ELK server is running? http://71.90.210.60:5601/app/kibana

