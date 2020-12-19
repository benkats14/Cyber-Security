# Cyber-Security
<img src="https://github.com/benkats14/Cyber-Security/blob/main/Diagrams/Network_diagram.pdf">
This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?

Availablity// We use SSH private key, and jumbox acts as a gateway to the other Vm on your created network. This is advantageous cuase it funnels all traffic through jumpbox only secure connections from allowed ip address using a SSH key.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

What does Filebeat watch for? 
Filebeat watches for log files/locations and collects log events.

What does Metricbeat record? 
Can install on your servers to periodically collect metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box|Gateway| 10.0.0.7 | Linux|
| Web-1     |Gateway  |10.0.0.5 |Linux|
| Web-2    |Gateway  |10.0.0.6 |Linux|
| Web-3    |Gateway  |10.0.09  |Linux|
| Elk         |Gateway  |10.1.0.4  |Linux|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
 75.7.117.107

Machines within the network can only be accessed by SSH.
Which machine did you allow to access your ELK VM? What was its IP address?
Jump_Box                      10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|Jump_Box|Yes|157.56.163.81|
|Web-1   |No |10.0.0.7|
|Web-2   |No|10.0.0.7|
|Web-3   |No|10.0.0.7|
|Elk      |No|10.0.07|

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

What is the main advantage of automating configuration with Ansible?
-you can put commands into many servers from a single playbook

The playbook implements the following tasks:
-In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install docker .io
- Install python3-pip
- Install Docker module
- Increse virtual memory
- Use more memory
- Download and launch a docker elk container 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-List the IP addresses of the machines you are monitoring

-Web-1| 10.0.0.5|

-Web-2|10.0.0.6|

-Web-3|10.0.0.9|

We have installed the following Beats on these machines:
-Specify which Beats you successfully installed
-Filebeat and Metribeat 
-Web-1| 10.0.0.5|
-Web-2|10.0.0.6|
-Web-3|10.0.0.9|

These Beats allow us to collect the following information from each machine:
 In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat: collects the log data and events
- Metricbeat: collects metrics and statistics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook..yml file to /etc/anisble.

- Update the hosts file to include
	[ weservers]
	10.0.0.5 ansible_python_interpreter=/usr/bin/python3
                10.0.0.6 ansible_python_interpreter=/usr/bin/python3
                10.0.0.9 ansible_python_interpreter=/usr/bin/python3
----------------------------------------------------------------------------------------
	[elk]
	10.1.0.4 ansible_python_interpreter=/usr/bin/python3
----------------------------------------------------------------------------------------
- Run the playbook:
	cd /etc/ansible/roles
	anisble-playbook-install-elk.yml  (elk)
	anisble-playbook-filebeat-playbook.yml      (webservers)
	anisble-playbook-metricbeat-playbook.yml (webservers)
-Navigate to htpp://40.88.8.180:5601/app/kibana to check that the installation worked as expected.

Answer the following questions to fill in the blanks:

-Which file is the playbook? Where do you copy it?
-/etc/ansible/roles/filebeat-config.yml

- Which file do you update to make Ansible run the playbook on a specific machine?
- /etc/ansible/hosts

 How do I specify which machine to install the ELK server on versus which to install Filebeat on?
-you specify the group [webservers] or [elk] at the end of the ansible-playbook command 

-Which URL do you navigate to in order to check that the ELK server is running?
- www.40.88.8.180:5601/app/kibana

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
- ansible-playbook filebeeat-myplaybook.yml
