# Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Azure_Cloud_Network.png![image](https://user-images.githubusercontent.com/83746458/139178737-72be87e4-31df-4f7d-a8f1-487b539d7013.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the 3 files may be used to install only certain pieces of it, such as Filebeat.

  [Install.elk.yml](https://github.com/supernova2801/Project-2-Elk-Stack/blob/main/Install.elk.yml)
  
  [Filebeat.playbook.yml](https://github.com/supernova2801/Project-2-Elk-Stack/blob/main/Filebeat.playbook.yml)
  
  [Metricbeat.playbook.yml](https://github.com/supernova2801/Project-2-Elk-Stack/blob/main/Metricbeat.playbook.yml)
  
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

Load balancing is the process of distributing the wight/availability a server recieves. This is useful in preventing a unusual amount of requests toward  a specific server. It helps in maintaining the availability of services during a DoS attack on the server.It can helps move weight from one server to another one in cases of it being uneven and unproportionate. Without one a server would just get overblown and end up crashing or being easily penetrated.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files, system logs & metrics.
- Filebeat collects data about the file system. It helps in detecting changes to files and recorded by tiestamps. If a hacker were to attempt to change a directory or file that info is then recorded and transmitted to the ELk server.

- Metricbeat collects the metrics of the operational state of a workstation on the network. some examples would be CPU usage, uptime, memory disks and more that getes sent to an output like logstash or elasticsearch.

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| VM-1     | Server   | 10.0.0.5   | Linux            |
| VM-2     | Server   | 10.0.0.6   | Linux            |
| VM-3     | Server   | 10.0.0.7   | Linux            |
| Elk-VM   | Monitoring| 10.1.0.4  | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the designated IP's via SSH. For example:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7
- 10.1.0.4

Machines within the network can only be accessed by the Jump-Box VM.
- Only the Jump-Box VM can connect to elk and its ip is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | Admins IP via SSH    |
| Web-1    | No/Only from Jmp-BX |   10.0.0.0/24.       |
| Web-2    | No/Only from Jmp-BX |   10.0.0.0/24.       |
| Web-3    | No/Only from Jmp-BX |   10.0.0.0/24.       |
| Elk-VM   | No/Only from Jmp-BX |   10.0.0.0/24.       |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It simplifies the proces pf configuring additional machines or updating changes to all existing ones to the network simultaneously. If need be we can make changes to the playbook and it automatically implements it to all the machines designated within the file. If there is no playbook we would have to make changes individually to the machines.

The playbook implements the following tasks:
- Installing the Docker container
- Installing Python-pip
- Installing Docker Python module
- Increases virtual memory
- Downloads and the launches the ELK container with ports 5044,5601,9200

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

 ![image](https://user-images.githubusercontent.com/83746458/139181820-f5aa2184-0da0-4757-8479-a55817010dad.png)
 
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1
- Web-2
- Web-3

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat collects data about the file system. It helps in detecting changes to files and recorded by tiestamps. They simplify compliling and the visiualization of log formats to a command by combinig automtic paths based on your OS. If a hacker were to attempt to change a directory or file that info is then recorded and transmitted to the ELk server. Filebeast can use instances like logstash or Elasticsearch.
-  Metricbeat collects the metrics of the operational state of a workstation on the network. some examples would be CPU usage, uptime, memory disks and more that getes sent to an output like logstash or elasticsearch.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Install.elk.yml file to /et/ansible/files.
- Update the hosts file to include the ELK server IP which os 10.1.0.4
- Run the playbook "Install.elk.yml" and navigate to http://(ELK server IP):5601/app/kibana to check that the installation worked as expected.

- The playbook is the install.elk.yml file and its copied in the /etc/ansible(or /etc/ansible/files) directory.
- _You have to update the host file in order to properly run the playbook on a machine
- You would go to the http://(ELK IP):5601/app/kibana

