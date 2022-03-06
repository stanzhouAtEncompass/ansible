# Ansible Architecture and Design
## Ansible configuration files
**Priority** 
1. ANSIBLE_CONFIG (Environment Variable, with a filename target)
2. ./ansible.cfg (An ansible.cfg file, in the current directory)
3. ~/.ansible.cfg (A hidden file, called .ansible.cfg, in the users home directory)
4. /etc/ansible/ansible.cfg (Typically provided, through packaged or system installations of Ansible)

## Inventories
[repo](https://github.com/spurin/diveintoansible/tree/master/Ansible%20Architecture%20and%20Design/Inventories)
## Modules
### The setup module
Used for gathering facts when executing playbooks
- This module is automatically executed, when using playbooks to gather useful information as variables, about remote targets. The information, can be used, during execution.
- The module, can also be executed directly, by the ansible command to find out the variables, available to a host
- Ansible provides many 'facts' about a target automatically
- This module, is also supported for Windows targets
- In Ansible 2.10, this been moved to ansible-base and is classed as a 'builtin' plugin. It can be referenced via the name 'setup' or 'ansible.builtin.setup'
- [Documentation](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/setup_module.html) 
`ansible centos1 -m setup`
### File Module
Used for file, symblinks and directory manipulation
- Sets attributes of files, symlinks and directories, or, removes files, symlinks and directories
- Many other modules support the same options as the 'file' module, including [copy], [template] and [assemble]

### Ansible Colors
Signifies success or failure, with or withou changes
- Red = Faiure
- Yellow = Success, with changes
- Green = Success, no changes
### Idempotency
An operation is idempotent, if the result of performing it once, is exactly the same as the result of performing it repeatedly without any intervening actions
### Copy Module
- The 'copy' module copies a file from the local or remote target, to a location on the remote target. Use the [fetch] module, to copy files from a remote target, to a local target.
- If you need variable interpolation in the cpoied files, use the [template] module.
### Command Module
- The 'command' module, takes the command name followed by a list of space-delimited arguments
- The given command will be executed on all selected nodes
- It is not processed through the shell, so, variables like $HOME and operations like <,>,|,; and &, will not work. Use the [shell] module if you need theres features
### ansible-doc
Manual pages for ansible
- Convenient and great alternative, to the online docs
- Try: ansible-doc file ; ansible-doc fetch
- Also provides you with the source code location, for modules , allowing you to understand, how a module works behind the scenes
