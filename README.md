# What is Ansible?
 
  Ansible is a radically simple IT automation platform that makes your applications and systems easier to deploy. Avoid writing scripts or custom code to deploy and update your applications— automate in a language that approaches plain English, using SSH, with no agents to install on remote systems. For anyone in the IT automation or DevOps engineer fields, learning the basics of Ansible is important.

## What Are the Benefits to Learning Ansible Basics?

  - A free and open-source community project with a huge audience.
  - Battle-tested over many years as the preferred tool of IT wizards.
  - Easy to start and use from day one, without the need for any special coding skills.
  - Simple deployment workflow without any extra agents.
  - Includes some sophisticated features around modularity and reusability that come in handy as users become more proficient.
  - Extensive and comprehensive official documentation that is complemented by a plethora of online material produced by its community.
  
# Ansible Basics

### Ansible Inventory:
  A list of managed nodes provided by one or more ‘inventory sources’. Your inventory can specify information specific to each node, like IP address. It is also used for assigning groups, that both allow for node selection in the Play and bulk variable assignment.

### Ansible Playbooks:
  A playbook is composed of one or more ‘plays’ in an ordered list. The terms ‘playbook’ and ‘play’ are sports analogies. Each play executes part of the overall goal of the playbook, running one or more tasks. Each task calls an Ansible module. Playbooks are expressed in YAML format with a minimum of syntax.

### Ansible Modules :
  The code or binaries that Ansible copies and executes on each managed node (when needed) to accomplish the action defined in each Task. Each module has a particular use, from administering users on a specific type of database to managing VLAN interfaces on a specific type of network device. You can invoke a single module with a task, or invoke several different modules in a playbook. Ansible modules are grouped in collections 
   
### Ansible Variables:
  Ansible uses variables to manage differences between systems. With Ansible, you can execute tasks and playbooks on multiple different systems with a single command. To represent the variations among those different systems, you can create variables with standard YAML syntax, including lists and dictionaries. You can define these variables in your playbooks, in your inventory, in re-usable files or roles, or at the command line. You can also create variables during a playbook run by registering the return value or values of a task as a new variable.
  
 ### Ansible Conditionals:
  In a playbook, you may want to execute different tasks, or have different goals, depending on the value of a fact (data about the remote system), a variable, or the result of a previous task. You may want the value of some variables to depend on the value of other variables. Or you may want to create additional groups of hosts based on whether the hosts match other criteria. You can do all of these things with conditionals. 

### Ansible Loops :
  Ansible offers the loop, with_, and until keywords to execute a task multiple times.
 
### Ansible Roles:
  A limited distribution of reusable Ansible content (tasks, handlers, variables, plugins, templates and files) for use inside of a Play. To use any Role resource, the Role itself must be imported into the Play.
