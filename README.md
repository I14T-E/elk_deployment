## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![network diagram](/diagrams/network_diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the ansible files may be used to install specific pieces of it. Click here for the [Anisble Files](https://github.com/I14T-E/elk_deployment/tree/master/ansible "Ansible Files").

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA (the D*mn Vulnerable Web Application).

Load balancing ensures that the application will be highly resilient, minimizing response time and maximizing throughput. In addition, the jump box aids in security as it restricts public acess to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to server logs and system system metrics.

The configuration details of each machine may be found below.


| Name       | Function | IP Address | Operating System |
|------------|----------|------------|------------------|
| Jump Box   | Gateway  | 10.0.0.1   | Linux            |
| Web-1      | Server   | 10.0.0.8   | Linux            |
| Web-2      | Server   | 10.0.0.6   | Linux            |
| Web-3      | Server   | 10.0.0.10  | Linux            |
| ELK Server | Server   | 10.1.0.4   | Linux            |


### Access Policies

The Jump Box (SSH) and ELK Server (HTTP) can accept direct connections from the internet. The three web servers on the internal network are not publically exposed and must be accessed through the load balancer.

All public internet connections are blocked by a firewall which only allows specific whitelisted IP addresses.

Machines within the network can only be accessed by the jump box. All updates and application deployments are done from here.

A summary of the access policies in place can be found in the table below.


| Name          | Publicly Accessible | Allowed IP Addresses           |
|---------------|---------------------|--------------------------------|
| Jump Box      | Yes                 | Must be on whitelist           |
| Web Servers   | No                  |  10.0.0.7                      |
| Load Balancer | Yes                 | Must be on whitelist           |
| ELK Server    | Yes                 | Must be on whitelist, 10.0.0.7 |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually. This allows for a simple and efficient setup that can be easily replicated.

The ELK playbook implements the following tasks:
- Installs docker
- Installs python3-pip
- Increases VM memory
- Downloads and starts docker ELK container

The following screenshot displays the result of running `sudo docker ps -a` after successfully configuring the ELK instance (run within elk server).

![elk docker ps command](/diagrams/elk_docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- web-1 (10.0.0.8)
- web-2 (10.0.0.6)
- web-3 (10.0.0.10)


The following beats have been installed on the web servers and allows us to collect information from each machine:
- Filebeat: General system log files
- Metricbeat: Statistics about the operating system and applications use
- Auditbeat: Security log events

For more information about each Beat, click on the respective link below.
- [Filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-overview.html "Filebeat")
- [Metricbeat](https://www.elastic.co/guide/en/beats/metricbeat/current/metricbeat-overview.html "Metricbeat")
- [Auditbeat](https://www.elastic.co/guide/en/beats/auditbeat/current/auditbeat-overview.html "Auditbeat")


### Using the Playbook
In order to use the playbook(s), you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Update the hosts file to include the local IP addresses under the proper group.
- Run the playbook, and navigate to the public address of your ELK machine (http://Your-ELK-VM-External-IP:5601/app/kibana) to check that the installation worked as expected.
- Troubleshoot as necessary
