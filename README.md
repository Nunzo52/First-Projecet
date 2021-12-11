## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Projcet1diagram](https://user-images.githubusercontent.com/87614983/145504214-08610290-272b-4a9e-995b-4a6ac3e726ee.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

 |“https://github.com/Nunzo52/Azure-Lab/blob/main/ELK.yml”|
 |"https://github.com/Nunzo52/Azure-Lab/blob/Ansible/ansible%20hosts"|
 |"https://github.com/Nunzo52/Azure-Lab/blob/Ansible/dvwa%20playbook"|
 |"https://github.com/Nunzo52/Azure-Lab/blob/Linux/ELK.yml"|
 |"https://github.com/Nunzo52/Azure-Lab/blob/Linux/filebeat.config.yml"|
 |"https://github.com/Nunzo52/Azure-Lab/blob/Linux/filebeat.yml"|
 |"https://github.com/Nunzo52/Azure-Lab/blob/Linux/metricbeat.config.yml"|
 |"https://github.com/Nunzo52/Azure-Lab/blob/Linux/metricbeat.yml"|

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
The 'Jump-Box' Server helps restrict backend accross to the network to a single point of entry on a separate external IP address. The 'Jump-Box' server uses an 'Ansible' container to run the 'playbook.yml' files to configure new and existing servers on the network.
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly AVAILABLE, in addition to restricting TRAFFIC to the network.
 
What aspect of security do load balancers protect? A Load Balancer ensures systems like Web1 and Web2 have trafic equally distributed to the most available server this ensures that whatever is being hosted has a high probability of being available.

What is the advantage of a jump box?
The 'Jump-Box' Server helps restrict backend accross to the network, if focusus traffic to a single entry point, this occurs on a separate external IP address. The 'Jump-Box' server uses an 'Ansible' container to run the its playbook YAML files to configure new and existing servers on the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the FILES and system METRICS.

FILEBEAT processes and watches System Logs for changes to system files.

METRICBEAT processes Logs and machine metrics including uptime, CPU, Memory and Traffic Loads.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Linux            |
| ELKSTACK | Cloud    | 10.4.0.4   | Linux            |
| Web1     | Webserver| 10.1.0.5   | Linux            |
| Web2     | Webserver| 10.1.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JUMPBOX machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
defined URL / IP address(es) ## JUMPOBXPROVISIONER-IP. Login to this system can only proceed with a pre-shared 'Public Key'.

Machines within the network can only be accessed by Machines within the network can only be accessed by the Jump-Box Server via the Ansible container running on the Jump Box.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|JumpBox   | Yes Port22          |(JumpBoxProvsioner-ip)|
|ELKSTACK  | Yes Port5601        |(Kibana-ip)           |
|ELKSTACK  | No Port22           |10.4.0.4              |
|Balancer  | Yes Port 80         |(JumpBoxProvsioner-ip)|
|Web1      | No Port 80          |10.1.0.4              |
|Web2      | No Port 80          |10.1.0.5              |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because with Ansible, one can very quickly rebuild an entire infrastructure. Which provides better quality assurance because all servers will be set up the same. It also will save the client time as changes occur so frequently. 

The playbook implements the following tasks:
... Downloads 'Images' to be installed on target machines.
... Installs software like Docker & Python 3 (PIP)
... Increases 'Virtual Memory' on target systems as needed.
... Publishes Required Ports such as: (tcp) 5044, 5601, 9200
... Download and install ELK Stack Container 
... Enable installed system to startup on reboot
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[image](https://user-images.githubusercontent.com/87614983/145685769-a422ef63-4fa0-4726-b761-0c602699c6d4.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
|Name	| Function |	IP Address |	Operating System |
|Web-1|Web Server|	10.1.0.5   |	Linux            |
|Web-2|Web Server| 10.1.0.6	  | Linux            |

We have installed the following Beats on these machines:

FILEBEATS
METRICBEATS

These Beats allow us to collect the following information from each machine:
Filebeats collect logs of file changes for the monitored system. Information is than sent to Logstash and Elastic Search. One Example is system.syslog that shows the boot process, it also collects metrics on the system such as CPU, Memory and Traffic Load and is used to generate reports. It reports on CPU Memory and metrics of the load. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

"https://github.com/Nunzo52/Azure-Lab/blob/Linux/filebeat.config.yml

Copy the 'filebeat_config.yml' and 'filebeat-playbook.yml' files to /etc/Ansible/files directory.

Make sure to update the 'host' IP address in lines 1106 and 1806 in the filebeats_config.yml file.

Run the playbook, and navigate to the Kibana Server URL to check that the installation worked as expected.

Run these commands to first change to the directory where the Elk.yml file will be saved. You will run the curl command to download the elk-server

cd /etc/ansible
curl -i href=“https://github.com/Nunzo52/Azure-Lab/blob/main/ELK.yml”
ansible-playbook /etc/ansible/Elk.yml
