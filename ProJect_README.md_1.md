## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!/Users/Rambo/Desktop/PROJECT-DIAGRAM-1.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml, metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly AVAILABLE, in addition to restricting ACCESS to the network.
- THEY PREVENT UNWANTED OR UNAUTHORIZED TRAFFIC FROM REACHING THE APPLICATION

What is the advantage of a jump box? _THEY PREVENT THE WEB SERVERS FROM BEING EXPOSED._ 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _CONFIG FILES_  and _SYSTEM FILES_.
- What does Filebeat watch for? LOG FILES
- What does Metricbeat record?_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.6   | Linux            |
| WEB-1    |WEBSERVERS| 10.1.0.5   | Linux            |
| WEB-2    |WEBSERVERS| 10.1.0.6   | Linux            |
| ELK-VM   |WEBSERVERS| 10.6.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _JUMP-BOX_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 10.142.242.51 

Machines within the network can only be accessed by _JUMP-BOX_.
- Which machine did you allow to access your ELK VM? MY PERSONAL COMPUTER 

What was its IP address? _107.142.242.51_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|-----------------------|--------------------|
| Jump Box | YES                   | 10.1.0.5 10.1.0.6  |
| WEB-1    | NO                    | 107.142.242.51     |
| WEB-2    | NO                    | 107.142.242.51     |
| ELK-VM   | YES                   | 107.142.242.51     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?_IT ALLOWS CHANGES TO BE MADE WITHIN ANY OF THE VMS ASSOCIATED TO IT.

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play.
- 1. INSTALL DOCKER.IO
- 2. INSTALL PYTHON3-PIP
- 3. INSTALL DOCKER PYTHON MODULE
- 4. DOWNLOAD AND LAUNCH A DOCKER WEB CONTAINER

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Update the path with the name of your screenshot of docker ps _(Desktop/Docker screenshot.png)_


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- List the IP addresses of the machines you are monitoring: 10.1.0.5 & 10.1.0.6

We have installed the following Beats on these machines:
- Specify which Beats you successfully installed: FileBeats & MetricBeats

These Beats allow us to collect the following information from each machine:
- FileBeats monitors log files and send them to either logstash or Elasticsearch for indexing. MetricBeat collects metric data from the target servers.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _ansible.conf_ file to _playbooks_.
- Update the _ansible host_ file to include...
- Run the playbook, and navigate to _jumpbox_ to check that the installation worked as expected. 

_Answer the following questions to fill in the blanks:_
- _Which file is the playbook? _elk-playbook.yml_ 
- _Which file do you update to make Ansible run the playbook on a specific machine? _elk-playbook.yml file_ 

- How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

- _Which URL do you navigate to in order to check that the ELK server is running? _https://20.150.136.217:5601/app/kibana_


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

install-elk.yml                                                                                                  
---

- name: Configure Elk VM with Docker
  hosts: elk
  remote_user: azadmin
  become: true
  port: 22
  tasks:

  - name: Install docker.io
    apt:
      update_cache: yes
      force_apt_get: yes
      name: docker.io
      state: present

  - name: Install python3-pip
    apt:
      force_apt_get: yes
      name: python3
      state: present


  - name: Install pip3
    apt:
      name: python3-pip
      state: present


  - name: Install Docker Module
    pip:
      name: docker
      state: present


  - name: Increase virtual memory
    command: sysctl -w vm.max_map_count=262144


  - name: Use More Memory
    sysctl:
      name: Sysctl -w vm.max_map_count
      value: 262144
      state: present
      reload: no



  - name: dwnload and launch a docker elk container
    docker_container:
      name: elk
      image: sebp/elk:761
      state: started
      restart_policy: always

      published_ports:
        - 5601:5601
        - 9200:9200
        - 5044:5044



RESULTS:
root@3c738a749487:/etc/ansible# ansible-playbook install-elk.yml 
[WARNING]: ansible.utils.display.initialize_locale has not been called, this
may result in incorrectly calculated text widths that can cause Display to
print incorrect line lengths

PLAY [Configure Elk VM with Docker] ********************************************

TASK [Gathering Facts] *********************************************************
ok: [10.6.0.4]

TASK [Install docker.io] *******************************************************
ok: [10.6.0.4]

TASK [Install python3-pip] *****************************************************
ok: [10.6.0.4]

TASK [Install pip3] ************************************************************
ok: [10.6.0.4]

TASK [Install Docker Module] ***************************************************
ok: [10.6.0.4]

TASK [Increase virtual memory] *************************************************
changed: [10.6.0.4]

TASK [Use More Memory] *********************************************************
ok: [10.6.0.4]

TASK [dwnload and launch a docker elk container] *******************************
[DEPRECATION WARNING]: The container_default_behavior option will change its 
default value from "compatibility" to "no_defaults" in community.docker 2.0.0. 
To remove this warning, please specify an explicit value for it now. This 
feature will be removed from community.docker in version 2.0.0. Deprecation 
warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [10.6.0.4]

TASK [Enable service docker on boot] *******************************************
ok: [10.6.0.4]

PLAY RECAP *********************************************************************
10.6.0.4                   : ok=9    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

 

metricbeat.yml  
---
- name: installing MetricBeat
  hosts: webservers
  become: yes
  tasks:

  - name: download MetricBeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/metricbeat/metricbeat-7.6.1-amd64.deb


  - name: install MetricBeat deb
    command: dpkg -i metricbeat-7.6.1-amd64.deb

  - name: copy MetricBeat
    copy:
      src: /etc/ansible/files/metricbeat.yml
      dest: /etc/metricbeat/metricbeat.yml

  - name: enable and configure docker module
    command: metricbeat modules enable docker

  - name: setup MetricBeat
    command: metricbeat setup

  - name: start MetricBeat service
    command: service metricbeat start

  - name: enable service MetricBeat on boot
    systemd:
      name: metricbeat
      enabled: yes




MetricBeat Results:
root@3c738a749487:/etc/ansible/roles# ansible-playbook metricbeat.yml  
[WARNING]: ansible.utils.display.initialize_locale has not been called, this
may result in incorrectly calculated text widths that can cause Display to
print incorrect line lengths

PLAY [installing MetricBeat] ***************************************************

TASK [Gathering Facts] *********************************************************
ok: [10.1.0.5]
ok: [10.1.0.6]

TASK [download MetricBeat deb] *************************************************
changed: [10.1.0.5]
changed: [10.1.0.6]

TASK [install MetricBeat deb] **************************************************
changed: [10.1.0.6]
changed: [10.1.0.5]

TASK [copy MetricBeat] *********************************************************
ok: [10.1.0.5]
ok: [10.1.0.6]

TASK [enable and configure docker module] **************************************
changed: [10.1.0.6]
changed: [10.1.0.5]

TASK [setup MetricBeat] ********************************************************
changed: [10.1.0.5]
changed: [10.1.0.6]

TASK [start MetricBeat service] ************************************************
changed: [10.1.0.6]
changed: [10.1.0.5]

TASK [enable service MetricBeat on boot] ***************************************
ok: [10.1.0.6]
ok: [10.1.0.5]

PLAY RECAP *********************************************************************
10.1.0.5                   : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
10.1.0.6                   : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   




filebeat-playbook.yml   
---
- name: installing and launching filebeat
  hosts: webservers
  become: yes
  tasks:

  - name: download filebeat deb
    command: curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.4.0-amd64.deb

  - name: install filebeat deb
    command: dpkg -i filebeat-7.4.0-amd64.deb

  - name: drop in filebeat.yml
    copy:
      src: /etc/ansible/files/filebeat-config.yml
      dest: /etc/filebeat/filebeat.yml


  - name: enable and configure system module
    command: filebeat modules enable system

  - name: setup filebeat
    command: filebeat setup


  - name: start filebeat service
    command: service filebeat start

  - name: enable service filebeat on boot
    systemd:
      name: filebeat
      enabled: yes


RESULTS:

root@3c738a749487:/etc/ansible/roles# ansible-playbook filebeat-playbook.yml 
[WARNING]: ansible.utils.display.initialize_locale has not been called, this
may result in incorrectly calculated text widths that can cause Display to
print incorrect line lengths

PLAY [installing and launching filebeat] ***************************************

TASK [Gathering Facts] *********************************************************
ok: [10.1.0.6]
ok: [10.1.0.5]

TASK [download filebeat deb] ***************************************************
changed: [10.1.0.6]
changed: [10.1.0.5]

TASK [install filebeat deb] ****************************************************
changed: [10.1.0.5]
changed: [10.1.0.6]

TASK [drop in filebeat.yml] ****************************************************
ok: [10.1.0.6]
ok: [10.1.0.5]

TASK [enable and configure system module] **************************************
changed: [10.1.0.5]
changed: [10.1.0.6]

TASK [setup filebeat] **********************************************************
changed: [10.1.0.5]
changed: [10.1.0.6]

TASK [start filebeat service] **************************************************
changed: [10.1.0.6]
changed: [10.1.0.5]

TASK [enable service filebeat on boot] *****************************************
ok: [10.1.0.6]
ok: [10.1.0.5]

PLAY RECAP *********************************************************************
10.1.0.5                   : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
10.1.0.6                   : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0