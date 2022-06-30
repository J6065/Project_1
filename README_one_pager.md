# AZURE Cloud Project

## Table of Contents

* REDAME.md(https://github.com/J6065/Project_1/blob/master/README.md)
* Images:
  * Network Diagram(https://github.com/J6065/Project_1/tree/master/Images)
  * Kibana sample data walkthrough (https://github.com/J6065/Project_1/tree/master/Kibana)
* YAML Playbooks(https://github.com/J6065/Project_1/tree/master/Playbooks)

## General Info

The following is a the documents, images, and information on a basic Azure cloud project. The project is based around two web servers behind a load balancer, with a jump box provisioner, docker containers, ELK server, accessible via SSH.

## Technologies

This project was created with:

* Azure
  * Load Balancer
  * 2 Web servers
  * 1 Jump box provisioner
  * 1 ELK server
* All servers running on Ubuntu Linux 18.04
* Docker/Ansible for backend server control/implementation
* Filebeat and Metricbeat
* Elasticsearch, Logstash, Kibana

## General Outline

One resource group was used for all servers. Two security groups (Red_Team and ELK server) were set up and peered for: (Red_Team) load balancer as public IP for web servers one and two, and the jump box provisioner; (ELK server) ELK server.
A docker container on the jump box was used as the method of command and control for the web servers and the ELK server. SSH security group rules only allow traffic routed to the jump box from a specific IP. Once there a docker container was used to set up playbooks and configuration for the web servers and ELK server. SSH to the web servsers and ELK server was only allowed through the docker container on the jump box.
Filebeat and metric beat were used to monitor web servers and monitoring data was sent to the ELK server. Kibana was accessed via web portal open only to one port and one IP address.
