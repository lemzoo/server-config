# Ansible Training from training.talkpython

## Ansible Core Concept
### Modules
Write your own module in your preferred language like python, java, etc.
For example: Clone a GIT repository

Go ahead see ansible documentations and also github

### Tasks
Written in YAML to tell ansible to execute an action
Task example:
- name: ensure Git is installed
  apt: name=git-core state=present update_cache=yes
  become: true # Use super user privelege
  
### Roles
Roles are a required file naming and directory convention for grouping tasks
and variables.
### Example of roles:
- base_directory/
  - deployment.yml
  - group_vars/
    - all
    - webserver
  - roles/
    - common/
      - tasks/
        - main.yml
        - git.yml
    - webserver/
      - tasks/
        - main.yml
        - nginx.yml
        
### Why user roles ?
Roles make groups of Ansible tasks reusable, both for different environments
and for usage between projects

### Playbooks
Playbooks are the top-level collection that contain one or more roles, many 
tasks, variables and all other information necessary for execution

### Example of playbooks
- base_directory/
  - hosts -> List of hosts where the playbook will be executed
  - deployment.yml
  - group_vars/
    - all
    - webserver
  - roles/
    - common/
      - tasks/
        - main.yml
        - git.yml
    - webserver/
      - tasks/
        - main.yml
        - nginx.yml

### Inventory
The Ansible inventory contains the list of servers to execute against and is 
typically grouped by role.
Default inventory is /etc/ansible/hosts

### Example inventory hosts file
[webserver]
- 192.168.1.1

[common]
- 192.168.1.1
- 192.168.24.1

[database]
- 231.8.1.44

[honeypot]
- 123.44.23.1

### Working with DATA
- Variables
- Reading environments variables
- Templates as input data
- Encrypting data

### Ansible templates
Jinja2 files that contain boilerplate text plus variables to produce output files.

For example: 
- Nginx configuration for a website
- PostgreSQL database configuration file
- Instructions customized to a servers's setup


### Encrypting sensitive data files
- ansible-vault
- ansible-vault encrypt
- ansible-vault decrypt

ansible-playbook --ask-vault-password ...
