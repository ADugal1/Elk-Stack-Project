# Elk-Stack-Project
The files in this repository were used to configure the network depicted below.
## Automated ELK Stack Deployment

{elk.yml}(https://richmond.bootcampcontent.com/Richmond-Boot-Camp/ur-rich-cyber-pt-10-2020-u-c/blob/master/%2013-Elk-Stack-Project/Activities/Stu_Day_1/Resources/install-elk.yml)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

The ansible-playbooks [elk.yml](https://richmond.bootcampcontent.com/Richmond-Boot-Camp/ur-rich-cyber-pt-10-2020-u-c/blob/master/%2013-Elk-Stack-Project/Activities/Stu_Day_1/Resources/install-elk.yml) and the [filebeat-playbook.yml](https://richmond.bootcampcontent.com/Richmond-Boot-Camp/ur-rich-cyber-pt-10-2020-u-c/blob/master/%2013-Elk-Stack-Project/Activities/Stu_Day_2/Resources/filebeat-config.yml) are needed to create and implement the Elk-Server

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
 - Beats in Use
 - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly scalable, in addition to restricting traffic to the network.
- The off-loading fucntion of a load balancer defends an organization agaisnt distributed denial-of-service attacks. It does this by shifting traffic from the corporate server to a public cloud provider, this case, Azure. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system system traffic.
- Filebeat watches for the log files & locations and collects log events
- Metricbeat records metric and statistical data from the operating system and from services running on the server

The configuration details of each machine may be found below.
| Name       | IP Address | Usage       | OS                   |
|------------|------------|-------------|----------------------|
| JumpBox    | 10.0.0.4   | Ansible     | Linux (ubuntu 18.04) |
| DVWA-VM1   | 10.0.0.5   | Docker-DVWA | Linux (ubuntu 18.04) |
| DVWA-VM2   | 10.0.0.6   | Docker-DVWA | Linux (ubuntu 18.04) |
| DVWA-VM3   | 10.0.0.7   | Docker-DVWA | Linux (ubuntu 18.04) |
| DVWA-VM4   | 10.0.0.8   | Docker-DVWA | Linux (ubuntu 18.04) |
| Elk-Server | 10.1.0.4   | ELK         | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Personal IP Address

Machines within the network can only be accessed by SSH connection
  The only machine that is able to connect to Elk-Server (10.1.0.4) is via JumpBox from private IP (10.0.0.4)
A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses   |
|------------|---------------------|------------------------|
| Jump Box   | No                  | Personal IP Only       |
| DVWA-VM1   | No                  | 10.0.0.4               |
| DVWA-VM2   | No                  | 10.0.0.4               |
| DVWA-VM2   | No                  | 10.0.0.4               |
| DVWA-VM2   | No                  | 10.0.0.4               |
| Elk-Server | No                  | 10.0.0.4 & Personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantages of automating configuration through Ansible is the ease of use and it's very easy to learn. Using Playbooks, you are able to configure multiple Machines through the use of a single command after initial configuration.

The playbook implements the following tasks:
- Create a New VM (should be named something simple "Elk-Server") Keep note of the Private IP (10.0.0.11) and the Public IP (0.0.0.0) you will need the Private IP to SSH into the VM and the Public IP to connect to the Kibana Portal (HTTP Site) to view all Metrics/Syslogs.
- Download and Configure the "elk-docker" container "In the hosts.conf you will need to add a new group [elkservers] and the Private IP (10.1.0.4) to the group. Then you need to create a new ansible-playbook (elk.yml) that will download, install, configures the "Elk-Server" to map the following ports [5601,9200,5044], and starts the contain
- Launch and expose the container "After installing and starting the new container. You can verify that the container is up and running by SSHing into the container from your JumpBox. Once you are in the [Elk-Server] run the command [sudo docker ps]
- Create new Inbound Security Rules to allow Ports: 5601 and 9200 "The Inbound Security Rules should allow access from your Personal Network"
- Open a new browser and type in the [Public IP:5601] to access the Kibana Portal Site


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- [10.0.0.5, 10.0.0.6, 10.0.0.7, 10.0.0.8}

We have installed the following Beats on these machines:
- Filebeat and Metricbeat
These Beats allow us to collect the following information from each machine:
- Filebeat is a leightweight shipper for forwarding and centralizing log data. Installed as an agent on your servers, Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat collects metrics from the operating system and from services running on the server. Metricbeat then takes the metrics and statistics that it collects and ships them to the output that you specify

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.yml and metricbeat.yml file to the /etc/ansible/roles/files/ directory.
- Update the configuration files to include the Private IP of the Elk-Server to the ElasticSearch and Kibana sections of the configuration file.
- Create a new ansible-playbook filebeat-playbook.yml in the /etc/ansible/roles/ directory that will install, drop in the filebeat.yml and metricbeat.yml files from the /etc/ansible/roles/files/ directory, uodate the configuration files, and start the service for both Filebeat and Metricbeat.
- Run the playbook, and navigate to ELk-Server to check that the installation worked as expected. [docker ps]
- The playbook is called filebeat-playbook.yml. You copy the file to the "/etc/ansible/hosts/" directory.
- The file you need to update is the filebeat.yml file which is a configuration file that will be dropped into the Elk-Server during the run of the ansible-playbook. When you update the host.cfg file in the ansible directory you will need to create a new group called [elkservers] and add the Private IP of the Elk-Server to the group. Then when configuring the filebeat.yml file you need to designate the Private IP of the Elk-Server in two lines of the .yml file. Lines 1106 and 1806 are the needed to be updated with the Private IP.
- The URL to use to verify the Elk-Server is running is the Public IP (0.0.0.0:5601)
