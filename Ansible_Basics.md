# Ansible Basics

## How Ansible Works

Link to RedHat's [article](https://www.ansible.com/overview/how-ansible-works)

Ansible is an IT automation engine that allows for automating of:
 - cloud provisioning
 - configuration management
    - ensures the consistency of all systems in the infrastructure is maintained
 - application deployment
   - applications are deployed automatically on a variety of environments
 - intra-service orchestration
 - etc.

Ansible uses YAML format, and uses no agents or additional custom security infrastructure.

It works by connecting to cloud nodes and pushing out small programs called **Ansible modules**. These programs are written to be resource models of the desired state of the system. Ansible then executes these modules over SSH (by default) and removes them upon completion. Nodes within the Ansible system are built and rebuilt in a matter of seconds.

Ansible has supports for various communication methods like Kerberos and passwords, thought SSH keys are most preferred. 

Ansible represents all the machines it manages using is a simple INI files that puts all of the managed machines in groups of the user's choosing.

## What is Ansible?

Link to Youtube [video](https://www.youtube.com/watch?v=wgQ3rHFTM4E)

### Configuration Models

In cloud automation there are two types of config models:

* Pull configuration: Nodes check with the server periodically and fetch the configuration from it. Requires nodes to have their own clients.
  * Used by Chef and Puppet
* **Push configuration**: Server pushes configuration to the nodes and forces compliance
  * Used by Ansible

### Ansible Architecture

* Local / main machine: Stores the various Ansible modules and inventory information, along with the Ansible software.
* Nodes: Systems to be configured
* Module: A collection of configuration code files called **playbooks**.
* Inventory: A document that groups the nodes under specific labels
* **Playbooks:** The core of the Ansible system. Playbooks are instructions that are used to configure the nodes
  * They are written in YAML (YAML Ain't Markup Language)

#### Playbook

Example of Ansible playbook ([Source](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html)):

```yaml
---
- name: Update web servers
  hosts: webservers
  remote_user: root

  tasks:
  - name: Ensure apache is at the latest version
    ansible.builtin.yum:
      name: httpd
      state: latest
  - name: Write the apache config file
    ansible.builtin.template:
      src: /srv/httpd.j2
      dest: /etc/httpd.conf

- name: Update db servers
  hosts: databases
  remote_user: root

  tasks:
  - name: Ensure postgresql is at the latest version
    ansible.builtin.yum:
      name: postgresql
      state: latest
  - name: Ensure that postgresql is started
    ansible.builtin.service:
      name: postgresql
      state: started
```

Playbooks begins with "---". A playbook is then subdivided into a list of plays, each is given:
- Name
  - Needs to correspond with the names in the inventory
- Hosts
  - The server we're targeting
- List of tasks
  -  Each element in the list is given a readable name followed by the instructions to execute the tasks (this could be anything from running specific terminal commands to make sure a service is online to changing the configuration of the service)

The local machine gathers the facts of each node (e.g. information about their state) and then push the playbooks to the nodes.

### Inventory File

A basic INI `/etc/ansible/hosts` inventory file may look something like this ([Source]()):

```text
mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```
The INI file can also be in YAML format like the following:

```yaml
all:
  hosts:
    mail.example.com:
  children:
    webservers:
      hosts:
        foo.example.com:
        bar.example.com:
    dbservers:
      hosts:
        one.example.com:
        two.example.com:
        three.example.com:
```

An inventory file classify nodes into groups. That way in our playbooks we can refer to groups of servers by one name, and Ansible will ensure of each of those servers in the group will get the same configuration. 

### Ansible Tower

Ansible by itself is a command line tool, while Ansible Tower is a framework that is built on top of Ansible. It provides an easy-to-use GUI that non-developers can use to create their desired environment according to their DevOps plan.