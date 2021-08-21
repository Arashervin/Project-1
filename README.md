## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://drive.google.com/drive/folders/1NBLc1ta995GjmCGu2ybRrHRaVBAJgwBs

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

 https://github.com/Arashervin/Project-1/tree/main/Ansible

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting authorized traffic to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?
Jumb box is the first line of deffence and verifys the authorized user to pass.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to resource usage and system availibility.
- _TODO: What does Filebeat watch for? Monitoring log files and events and keeping track of logs
- _TODO: What does Metricbeat record? Monitoring in higher scale such as database, collecting the statistics and information

The configuration details of each machine may be found below.
_https://drive.google.com/drive/folders/1NBLc1ta995GjmCGu2ybRrHRaVBAJgwBs

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    | Webserver|  10.1.0.5  | Linux            |
| Web-2    | Webserver|  10.1.0.6  | Linux            |
| Web-3    | Webserver|  10.1.0.7  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _192.27.100.23

Machines within the network can only be accessed by 10.0.0.0/16
***

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 192.27.100.23        |
|Web-1,2,3 | No                  |    N/A                  |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
Consistancy and no human error - more efficient and time saving

The playbook implements the following tasks:

- Installs Docker
- Installs Pip3 (Python)
- Install Python Docker Module
- Tells the system to use more memory
- Downloads and launches a docker elk container on elk server
- Enables the docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
https://github.com/Arashervin/Project-1/blob/main/GitHub%20shot1.PNG


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1,2,3  Load Balancer & Jump box VM

We have installed the following Beats on these machines:
Filebeats on web servers 1-3. Metricbeat on web servers 1-3

These Beats allow us to collect the following information from each machine:
Filebeat collects log data for our web servers and forwards them to our elk server so that we may track and analyze them in Kibana. 
It is essentially a log forwarding tool that itemized and tracks all files on the server and reports changes to them.

Metricbeat. We expect to collect a wide assortment of data from which coutries accessed the web servers, when and what they downloaded. 
It will also show up geographically where are vistors come from and what time they visited as well as the filetype in which they downloaded. 
Metric beat shows us advanced metrics that we can use to better understand when, where and what our visitors are doing on our website


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the YML file to /etc/ansible/roles/.
- Update the YML file to include the details.
- Run the playbook, and navigate to distination directory to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
Filebeat-playbook.yml - /etc/filebeat/filebeat.yml Metricbeat-playbook.yml - /etc/metricbeat/metricbeat.yml
- _Which file do you update to make Ansible run the playbook on a specific machine?
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?  Hosts
By including the IP address inside the file.
- _Which URL do you navigate to in order to check that the ELK server is running?
 http://localhost:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
Filebeat
curl
https://github.com/Arashervin/Project-1/blob/main/Bonus%20file

then you cat filebeat.config update it the ip address of your elk server so that when you install filbeat + Metric beat on web 1-3 it send its to your elk server.

Nano the hosts and make sure web 1-3 is made under a web servers group [webservers] you need to use the private's ip addresses of the web 1 - 3 under [webservers]