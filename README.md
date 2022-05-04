# README

### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _playbook_ file may be used to install only certain pieces of it, such as Filebeat.

- _TODO: Enter the playbook file._

This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _availible_, in addition to restricting _inbound access_ to the network.

- _TODO: What aspect of security do load balancers protect?_
 Availability by providing balanced access to both web servers and insuring access to one of the web servers if one goes down. Accessibility by only allowing authourized users to access the web servers.

_What is the advantage of a jump box?_ The Jump Box controles authorized access to the network via SSH login, with Docker and ansible for networked server control and access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for _changes to the file systems of the VMs on the network_ and system _system metrics_.

- _TODO: What does Filebeat watch for?_ Filebeat detects changes to the filesystem.
- _TODO: What does Metricbeat record?_ Metricbeat detects changes in system metrics, such as CPU usage. We use it to detect SSH login attempts, failed `sudo` escalations, and CPU/RAM statistics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
|DVWA(Web1)|Web Server| 10.0.0.5   | Linux            |
|DVWA(Web2)|Web Server| 10.0.0.6   | Linux            |
| ELK      |Monitoring| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the _jump box_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- _TODO: Add whitelisted IP addresses_  204.195.65.104

Machines within the network can only be accessed by _each other_.

- _TODO: Which machine did you allow to access your ELK VM?_ The docker image from the jump box via the private IP is allowed access to the ELK server. Web1 and Web2 servers send traffic to the ELK server for monitoring.

  _What was its IP address?_ The jump box IP is 10.0.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 204.195.65.104       |
| ELK      | Yes                 | 204.195.65.104       |
|DVWA(Web1)| No                  | 10.0.0.4             |
|DVWA(Web2)| No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- _TODO: What is the main advantage of automating configuration with Ansible?_ Less chance of human error and the abillity to configure multipule machines at the same time.

The playbook implements the following tasks:

- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...Install docker.IO; name: docker.io
- ...Install pip3; name: python3-pip
- ...Install docker python module; name: docker
- ...Use more memory; name: vm.max_map_count
- ...Download and launch a docker ELK container; name: elk

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- _TODO: List the IP addresses of the machines you are monitoring_ Web_1: 10.0.0.5 and Web_2: 10.0.0.6

We have installed the following Beats on these machines:

- _TODO: Specify which Beats you successfully installed_
I have installed Filebeat and Metricbeat.

These Beats allow us to collect the following information from each machine:

- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat monitors changes to the filesystem. Metricbeat looks for changes in system metrics and to detect SSH login attempts, `sudo` escalations, and CPU/RAM statistics.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: The docker container in the jump box is the control node.

SSH into the control node and follow the steps below:

- Copy the _playbooks_ file to _the Ansible control Node_.
- Update the _hosts_ file to include... the web servers and the elk server.
- Run the playbook, and navigate to _<http://104.210.66.105:5601/app/kibana>_ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_

- _Which file is the playbook? Where do you copy it?_ The file path for the playbooks: `/etc/ansible/` ; the files are `elk_install.yml` `filebeat-playbook.yml` and `metricbeat.yml`.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ Via the hosts file [webservers]: 10.0.0.5 and 10.0.0.6; [elk]: 10.1.0.4.
- _Which URL do you navigate to in order to check that the ELK server is running?_ <http://104.210.66.105:5601/app/kibana>

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._