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
- Saltstack - 
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










