## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Jesse-Mendoza/Automated-Elk-Stack-Deployment/blob/main/Diagrams/RedTeam-Network-Diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project 1 Red-Team Network Diagram file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/Jesse-Mendoza/Automated-Elk-Stack-Deployment/tree/main/Ansible

This document contains the following details:

    • Description of the Topology
    
    • Access Policies
    
    • ELK Configuration
        - Beats in Use
        - Machines Being Monitored
    
    • How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to filtering access to the network.

    • Load balancing ensures that the application will be highly available and adds resiliency by
      distributing live traffic evenly across multiple servers, effectively eliminating single points
      of failure from attacks such as DDoS attacks.

    • The advantage of the Jump Box is that it provides a gateway router to the private network,
      ensuring that all other machines in the network do not directly face the internet, providing
      a more secure network.
          
          
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.

    • Filebeat monitors the log files or locations that you specify, collects log events, and forwards them
      either to Elasticsearch or Logstash for indexing. The data can be viewed and analyzed with Kibana.

    • Metricbeat collects metrics from the operating system and from services running on the server.
      Metricbeat then takes the metrics and statistics that it collects and ships them to Elasticsearch to be
      processed by Logstash, and can be viewed and analyzed with Kibana.


The configuration details of each machine may be found below.

| Name       |    Function    | IP Address | Operating System |
|------------|----------------|------------|------------------|
| Jump Box   | Gateway        | 10.0.0.4   | Linux            |
| Web-1 DVWA | Server         | 10.0.0.5   | Linux            |
| Web-2 DVWA | Server         | 10.0.0.6   | Linux            |
| Web-3 DVWA | Server         | 10.0.0.7   | Linux            |
| ELK-SERVER | Monitoring     | 10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

  
    • The Jump Box Machine may be accessed from IP address 73.96.160.169 


Machines within the network can only be accessed by the Jump Box.

    • The ELK server may be accessed from Jump Box   // 10.0.0.4
    
    • The ELK server may be accessed from Web-1 DVWA // 10.0.0.5    
    
    • The ELK server may be accessed from Web-2 DVWA // 10.0.0.6  
    
    • The ELK server may be accessed from Web-3 DVWA // 10.0.0.7  


A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible |              Allowed IP Addresses            |
|------------|---------------------|----------------------------------------------|
| Jump Box   | No                  | 73.96.160.169                                |
| Web-1 DVWA | No                  | 10.0.0.4                                     |
| Web-1 DVWA | No                  | 10.0.0.4                                     |
| Web-2 DVWA | No                  | 10.0.0.4                                     |
| ELK-SERVER | No                  | 10.0.0.4 // 10.0.0.5 // 10.0.0.6 // 10.0.0.7 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

    • Automating configuration with ansible ensures provisioning scripts run identically everywhere,
      every time they run. This eliminates as much variability between configurations as possible,
      and allows for easy installation of multiple versions of a tool(s) to be used at the same time
      accross different projects.

The playbook implements the following tasks:

    • Configure Elk VM with Docker
    
    • Install docker.io
    
    • Install pip3
    
    • Install Docker python module
    
    • Download and launch a Docker elk container sebp/elk:761
    
    • Use systemctl to increase memory
    

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/Jesse-Mendoza/Automated-Elk-Stack-Deployment/blob/main/Images/Docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
       
    • Web-1 DVWA // 10.0.0.5 
    
    • Web-2 DVWA // 10.0.0.6
    
    • Web-3 DVWA // 10.0.0.7

We have installed the following Beats on these machines:
    
    • Filebeat  
    
    • Metricbeat

These Beats allow us to collect the following information from each machine:

    • Filebeat plays the role of the logging agent; installed on the machine generating the log files,
      tailing them, and forwarding the data to either Logstash for more advanced processing or directly
      into Elasticsearch for indexing.
      
    • Metricbeat is used for monitoring server performance within an environment, as well as that of
      different external services running on them. For example, Metricbeat can be used to monitor and
      analyze system CPU, memory and load.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

     • Copy the Filebeat and Metricbeat configuration files to '/etc/ansible'
     
     • Update the configuration files to include your ELK-SERVER's private IP address: 
       (filebeat-config.yml: lines 1106 & 1806, metricbeat-config.yml: lines 62 & 96)

     • /etc/ansible/filebeat-playbook.yml is the Filebeat playbook. Copy it to '/etc/ansible'

     • /etc/ansible/metricbeat-playbook.yml is the Metricbeat playbook. Copy it to '/etc/ansible'

     • To make Ansible run the playbook on a specific machine(s), update the '/etc/ansible/hosts' inventory file to include: 

          [Group name]
          
            e.g. [webservers] // [elk]

          [Private IP addresses of webservers] [location of a Python 3 interpreter]
          
            e.g. 'x.x.x.x ansible_python_interpreter=/usr/bin/python3'
            
     • Command to run playbook: ansible-playbook [playbook.yml] 

Run each playbook, then navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.

