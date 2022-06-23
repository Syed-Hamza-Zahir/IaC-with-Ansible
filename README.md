# IaC-with-Ansible

## Infastructure as Code (IaC)
https://www.redhat.com/en/topics/automation/what-is-infrastructure-as-code-iac

Infrastructure as Code (IaC) is the managing and provisioning of infrastructure through code instead of through manual processes.

Automating infrastructure provisioning with IaC means that developers don’t need to manually provision and manage servers, operating systems, storage, and other infrastructure components each time they develop or deploy an application. Codifying your infrastructure gives you a template to follow for provisioning.

## Benefits:
IaC can manage IT infrastructure needs while also improving consistency and reducing errors and manual configuration.

Benefits:
- Cost reduction
- Increase in speed of deployments
- Reduce errors 
- Improve infrastructure consistency
- Eliminate configuration drift

What is configuration drift in Devops?
Configuration drift refers to an environment in which running clusters in an infrastructure become increasingly different over time, usually due to manual changes and updates on individual clusters

## IaC tools
Server automation and configuration management tools can often be used to achieve IaC. There are also solutions specifically for IaC. 

These are a few popular choices:
- Progress Chef - Progress Chef is a configuration management tool written in Ruby and Erlang.
- Puppet - Puppet is an open source software configuration management and deployment tool. It'sused to pull the strings on multiple application servers at once. B
- Red Hat Ansible Automation Platform - 
- Saltstack - Salt is Python-based, open-source software for event-driven IT automation, remote task execution, and configuration management.
- Terraform - HashiCorp Terraform is an open source infrastructure as code (IaC) software tool that allows DevOps engineers to programmatically provision the physical resources an application requires to run. 
- AWS CloudFormation - 
- Ansible 

# What is configuration management and orchestration under IaC
Orchestration is the automated configuration, management, and coordination of computer systems, applications, and services. Orchestration helps IT to more easily manage complex tasks and workflows. IT teams must manage many servers and applications, but doing so manually isn't a scalable strategy.

# What is ansible
Ansible is a python-based open source IT Configuration Management, Deployment & Orchestration tool.

Ansible Automation Platform can be used to provision operating systems and network devices, deploy applications, and manage configuration.
 Key benefits:
 - Very simple to set up and use: No special coding skills are necessary to use Ansible's playbooks (more on playbooks later). 
 - Powerful: Ansible lets you model even highly complex IT workflows. Flexible: You can orchestrate the entire application environment no matter where it's deployed.
 - Ansible is angentless because we only need to have ansible installed on the controller. 
- We connect using SSH - this also adds to its simplicity

# Ad Hoc Commands

##  Common Flags
- ``-m`` the module being used
- ``-i`` path to inventory
- ``-a`` to pass arguements
- ``-l`` limit to specific host from inventory

## Examples

### Ping module
``ansible -m ping all -i hosts``

### Service module
``ansible -i hosts -m service -a 'name=apache2 state=restarted' host1.example.org``

### Shell module
``ansible -i hosts -m shell -a 'grep DISTRIB_RELEASE /etc/lsb-release' all``

 ``all`` is a shortcut meaning ``all hosts found in inventory file``

### Copy module
``ansible -i hosts -m copy -a 'src=/etc/motd dest=/tmp/' host0.example.org``

With this module you can copy a file from the controlling machine to the node.

### Setup module
``ansible -i hosts -m setup -a 'filter=ansible_memtotal_mb' all``

The setup module specializes in node's facts gathering -- getting information aboyt the node.

When using the setup module, you can use ``*`` in the ``filter=`` expression.

## Selecting hosts

We saw that all means 'all hosts', but ansible provides a lot of other ways to select hosts: http://docs.ansible.com/ansible/latest/intro_patterns.html

- ``host0.example.org:host1.example.org`` would run on host0.example.org and host1.example.org
- ``host*.example.org`` would run on all hosts starting with 'host' and ending with '.example.org'

# Yaml file to provision web server
```
---


- hosts: web
  gather_facts: yes
  become: true

  tasks:
  - name: Update and upgrade apt packages
    become: true
    apt:
      upgrade: yes
      update_cache: yes

  - name: Copy app into web virtual machine
    synchronize:
      src: ~/eng114_devops
      dest: /home/vagrant

  - name: install nginx
    apt: name=nginx state=present

  - name: Reverse proxy
    copy:
      src: ~/eng114_devops/default
      dest: /etc/nginx/sites-available/default

  - name: install git
    apt: name=git state=present

  - name: Add Nodesource Keys
      become: yes
    apt_key:
      url: https://deb.nodesource.com/gpgkey/nodesource.gpg.key
      state: present

  - name: Add Nodesource Apt Sources
    become: yes
    apt_repository:
      repo: '{{ item }}'
      state: present
    with_items:
      - 'deb https://deb.nodesource.com/node_6.x xenial main'
      - 'deb-src https://deb.nodesource.com/node_6.x xenial main'

  - name: Install NodeJS
    become: yes
    apt:
      name: nodejs
      state: latest
      update_cache: yes

  - name: Install NPM
    apt: pkg=npm state=present


  - name: install pm2
    npm:
      name: pm2
      global: yes
```

Run the following to get the lastest versions of npm and node on the web machine 
```
- sudo npm start

- sudo npm i

- sudo rm -rf node_modules/

- sudo npm install -g npm@lastest

- sudo n stable

- sudo npm install -g n

-  npm cache clean -g n
```





