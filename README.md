# Cloud-Security-Administartion
Azure cloud security network diagram and scripts
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!![Azure_Network_Diagram](https://user-images.githubusercontent.com/89329304/148301750-3e7797f1-10d8-40d4-8bf7-815e506a8f05.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML_ file may be used to install only certain pieces of it, such as Filebeat.

[Ansible Playbooks](https://drive.google.com/drive/folders/1g2Fd8K3v1uw2_Y1VN8LVALgtvCYTF7LO?usp=sharing)


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly **protected**_, in addition to restricting **strain and unauthorized access**_ to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box?_ Load balancers help with protecting the primary webservers from traffic overload. This is done by redirecting traffic from one server that is being flooded with trafiic to another capable pool of servers meant to releive the load on the network and distribute the load across multiple servers. a JumpBox ensures that the only point of access from the internet if the JumpBox. There is no way to access or navigate through the network without first landing in the JumBox

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **configuration files**_ and system **files**_.

-What does Filebeat watch for?_Filebeat monitors log files and events specified by the user. These files are gatherd for reveiw using external tools duch as logstash or Elastisearch for documentation. 

-What does Metricbeat record?_Metricbeat takes gathered data and sends it to a specified output. Metricbeat can automatically insert gathered data directly into Elasticsearch or Logstash for documentation.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function  | IP Address | Operating System |
|----------|-----------|------------|------------------|
| Jump Box | Gateway   | 10.0.0.1   | Linux            |
| Web1     | DVWA1     | 10.0.0.5   | Linux            |
| Web2     | DVWA2     | 10.0.0.6   | Linux            |
| ELK      | ELK/Kibana| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox Provisioner_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.176.50.219

Machines within the network can only be accessed by JumpBox_.
- Which machine did you allow to access your ELK VM? What was its IP address?_My personal host machine (IP:67.176.50.219)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses     |
|----------|---------------------|--------------------------|
| Jump Box | Yes                 | 67.176.50.219            |
| Web1     | No                  | 10.0.0.4 & 10.0.0.5      |
| Web2     | No                  | 10.0.0.4 & 10.0.0.6      |
| ELK      | Yes (HTTP)          | 10.1.0.4                 |
| ELK      | Yes (HTTP)          | 10.1.0.4 & 67.176.50.219 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?_Ansible playbooks are the main advantage because playbooks allow for automated configuration of services across all machines within a network using that container. This means that all the DVWA's can be configured consistantly and simultaneously instead of individually. 

The playbook implements the following tasks:
- Install docker.io on the virtual machine
- install python3-pip
- Install Docker module
- Dowload and launch docker Elk container
- Enable service docker on startup/boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![sudo docker ps -a](https://user-images.githubusercontent.com/89329304/148287830-14c3ca64-2b82-4695-8464-6f05820c5a06.png)

 
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 (10.0.0.5) and Web2 (10.0.0.6)

We have installed the following Beats on these machines:
-Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._Filebeat monitors log files and log events. Metricbeat monitors for any information in the file system that has been tampered or manipulated and automatically sends it to Elasticsearch for documentation and review. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible configuration_ file to run the playbook_.
- Update the ansible host_ file to include the Ip addresses of machines that filebeat and metricbeat will be deployed on. 
- Run the playbook, and navigate to Web1 and Web2_ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_*.yml files are playbook files
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
