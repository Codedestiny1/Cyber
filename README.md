# Cyber
Cybersecurity

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/Codedestiny1/Cyber/blob/main/Images/Diagram_ELKStack.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.

- [Install Elk](https://github.com/Codedestiny1/Cyber/blob/main/Ansible/install-elk.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
- Beats in Use
- Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available and scalable, in addition to restricting access to the network.
-Load balancers protect the confidentiality aspect of the CIA Triad by providing a public IP address to mask backend resources from direct internet access
-The advantage of our jump box is that it acts as our gateway router between VMs on a network. Securing and monitoring this single gateway allows us to focus ont he single connnection to the jump box instead of multiple connections between all the virtual machines. Like the load balancer, the jump box is exposed to the public internet, sits in front of other machines that are not exposed to the public internet, and controls access to the virtual machines by allowing connections from specific IP addresses and forwarding them to the back end resources. To secure the jump box we limit the number of machines it can access, lock the root account and limit sudo access of the administrator account on the jump box, implement log monitoring on the jump box, add two factor authentication for SSH login to the jump box, implement a host firewall (UFW or IPtables(RedTeam-SG)) on the jump box, and limit the jump box network access within the virtual private network (RedTeamNet/ELKNet).

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system (log files (Filebeat)) and system metrics (Metricbeat). ELK server does this through Beats (Open source data shippers). We will be utilizing two (2) beats Filebeat and Metricbeat. Not covered in this topology is six (6) other beats that can be configured on the ELK server (Auditbeat for audit data, Functionbeat for cloud data, Heartbeat for Availability, Journalbeat for Systemd journals, Packbeat for network traffic, and Winlogbeat for windows event logs).
-Filebeat collects log streams including their pod, container, node, VM, host, and other metadata for automatic correlation. It detects new containers and monitors them.
-Metricbeat collects system-level CPU usage, memory, filesystem, disk IO, network IO statistics, as well as statistics for every process running on the systems.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name                 | Function                                 | IP Address | Operating System      |
|----------------------|------------------------------------------|------------|-----------------------|
| Jump-Box-Provisioner | Gateway Router                           | 10.0.0.4   | Linux 1vCPUs 1GiB Ram |
| Web-1                | Webserver                                | 10.0.0.7   | Linux 1vCPUs 2GiB Ram |
| Web-2                | Webserver                                | 10.0.0.8   | Linux 1vCPUs 2GiB Ram |
| ELK-Server           | Database for Network Security Monitoring | 10.1.0.5   | Linux 2vCPUs 8GiB Ram |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 174.56.226.201

Machines within the network can only be accessed by SSH (port 22) and HTTP (port 80).
- Jump-Box-Provisioner can access the ELK Server from the Public IP address 174.56.226.201

A summary of the access policies in place can be found in the table below.

| Name                 | Publicly Accessible | Allowed IP Addresses |
|----------------------|---------------------|----------------------|
| Jump-Box-Provisioner |        Yes          |    174.56.226.201    |
| Web-1                |        No           |    10.0.0.4          |
| Web-2                |        No           |    10.0.0.4          |
| ELK-Server           |        No           |    10.0.0.4          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because we have created a code that contains the configuration of a server. That code can be version controlled and easily audited.
-The main advantage of automating configuration with Ansible is the ability to install software and change configuration files in thousands of servers within a few minutes.

The playbook implements the following tasks:
- Install docker.io downloads the software package for the Docker engine used for running containers.
- Install python3-pip downloads the software package used to install Python software. 
- Install Docker Module initiates the python client for Docker which is required by Ansible to control the state of Docker containers.
- Increase Virtual memory sets the ELK Server to use more memory to allow the ELK container to run.
- Use more memory uses Ansible's sysctl module to configure the increased virtual memory everytime the VM has been restarted.
- Download and launch a docker elk container downloads the docker contained called sebp/elk:761. sebp is the organization that made the container. elk is the container. 761 is the version. 5601:5601, 9200:9200, 5044:5044 configures the container to start with those port mappings. State: Started - starts the container.
- Enable service docker on boot allows the docker service to start up automatically if you restart the ELK machine.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker PS Output](https://github.com/Codedestiny1/Cyber/blob/main/Images/DockerPS.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
