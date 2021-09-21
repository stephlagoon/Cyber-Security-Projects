## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![Stephanie-Azure-Diagram drawio](https://user-images.githubusercontent.com/78007547/134023423-a4692690-6ae1-4679-b10a-efeb2891e2f1.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available by forwarding traffic from port 80 (based on my network) to the backend pool, in addition, the jump box server functions to restrict access to the network to authorized users.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system log files in web-1 and web-2 virtual networks using Filebeat software in addition to machine metrics, such as uptime with metricbeat software.


The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box |Gateway    | 10.0.0.4  |Linux/Ubuntu 18.04|
| Web-1    |Webserver  | 10.0.0.5  |Linux/Ubuntu 18.04|
| Web-2    |Webserver  | 10.0.0.6  |Linux/Ubuntu 18.04|
|Elk-Server|Webserver  | 10.1.0.4  |Linux/Ubuntu 18.04|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: Home Network IP address.


Machines within the network can only be accessed by the Jump-Box Provisioner (10.0.0.4).

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  Home IP             |
| Web 1    | No/Yes              |  Home IP & 10.0.0.4  |
| Web 2    | No/Yes              |  Home IP & 10.0.0.4  |
| ELK      | No/Yes              |  Home IP & 10.0.0.4  |

### Elk Configuration

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows you to configure multiple machines simultaneously while also minimizing errors.


The playbook implements the following tasks:
- Install docker.io using apt module.
- Install python3-pip using apt module.
- Install docker module using the pip module.
- Increase virtual memory using sysctl module.
- Download and launch a docker elk container using docker_container module.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


![TODO: Update the path with the name of your screenshot of docker ps output](Images/ps-screenshot)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 (10.0.0.5)
- Web-2 (10.0.0.6)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect only the necessary data points. ELK supports eight beats. Two of the beats utilized in this project were Filebeat and Metricbeat. Filebeat collects data about the file system, including which files have been changed, as well as when they were changed. Additionally, Filebeat can monitor suspicious activity. This leaves a trace that can be followed and investigated using logs if an attacker strikes the network. Suspicious activity includes brute force logins, as well as logins from IPs outside of the network. Filebeat, then, helps generate and organize these log files to send to Logstash and Elasticsearch in a GUI interface to help visualize Elasticsearch data with charts and graphs. Metricbeat, however, collects machine metrics from the operating system and services running on the server. Metricbeat can analyze things like CPI, memory, and load from the operating system. Metricbeat can help monitor our servers by collecting metrics from the systems running on the server, such as services like Apache and MySQL.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to etc/ansible/roles/install-elk/tasks.

- Update the etc/ansible/hosts file to include the groups specified in brackets [Elk], in addition to the Elk-Server IP address "10.1.0.4" followed by ansible_python_interpreter=usr/bin/python3.

- Run the playbook, and navigate to  http://[elk-server-ip]:5601/app/kibana#/home to check that the installation worked as expected.

Use the following command to run, download the playbook, update the files, etc.:

#
## Download Repo
`git clone [URL_to_Repo: https://github.com/stephlagoon/ELK-Stack-Project.git]`

## Get Updates from Repo
`git pull`


## Update files and push to repo
### To add all files
`git add . `
### To add specific files
`git add [specific filename]`
### To commit files with message
`git commit -m "insert message here"`
### Push commits to repo
`git push origin --set-upstream <-branch->`

## Commands to start Ansible container

### command to list container
`docker container list -a`

### command to open Ansible container
`sudo docker start [container_name]`

`sudo docker attach [container name]`

### command to run the playbook
`ansible-playbook [playbook_name.yml]`







