# Ansible Playbooks
## YAML
- YAML is a data-oriented language, as a human readable, data-serialisation lanuage
- Easy to use, easy to read, great for collaboration
- Reading and writing of YAML, supported in most major programming languages
- Often seen with a .yaml or .yaml extension, .yaml is officially the recommended extension since 2006
### qutoes
**only the double quotes will be work**, eg:
``` bash
$ cat test.yaml 
# Every YAML file should start with three dashes
---

no_quotes: this is a string example\n
double_quotes: "this is a string example\n"
single_quotes: 'this is a string example\n'
 
# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/04$ ./show_yaml_python.sh 
{'double_quotes': 'this is a string example\n',
 'no_quotes': 'this is a string example\\n',
 'single_quotes': 'this is a string example\\n'}
```
### multiple lines
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/05$ cat test.yaml 
# Every YAML file should start with three dashes
---

example_key_1: |
  this is a string
  that goes over
  multiple lines
 
# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/05$ ./show_yaml_python.sh 
{'example_key_1': 'this is a string\nthat goes over\nmultiple lines\n'}
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/05$ python3
Python 3.8.10 (default, Nov 26 2021, 20:14:08) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print('this is a string\nthat goes over\nmultiple lines\n')
this is a string
that goes over
multiple lines

```
### greater then sign(to use multi plines in YAML to represent as a single ine in both ansible and python)
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/06$ cat test.yaml 
# Every YAML file should start with three dashes
---

example_key_1: >
  this is a string
  that goes over
  multiple lines
 
# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/06$ ./show_yaml_python.sh 
{'example_key_1': 'this is a string that goes over multiple lines\n'}
```
### greater then sign with an additional minus
removed the ending carriage return
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/07$ cat test.yaml 
# Every YAML file should start with three dashes
---

example_key_1: >-
  this is a string
  that goes over
  multiple lines
 
# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/07$ ./show_yaml_python.sh 
{'example_key_1': 'this is a string that goes over multiple lines'}
```
### integer
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/08$ cat test.yaml 
# Every YAML file should start with three dashes
---

example_integer: 1
 
# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/08$ ./show_yaml_python.sh 
{'example_integer': 1}
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/08$ python3
Python 3.8.10 (default, Nov 26 2021, 20:14:08) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> myvar = {'example_integer': 1}
>>> print(myvar['example_integer'])
1
>>> print(type(myvar['example_integer']))
<class 'int'>
```
If we quote the integer value, it makes it into a string rather than an integer.
### booleans
YAML is very versatile with how it can handle booleans
go for a clear true or false with a capital letter and lowercase.
### List items
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/11$ cat test.yaml 
---
# Every YAML file should start with three dashes

- item 1
- item 2
- item 3
- item 4
- item 5

# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/11$ ./show_yaml_python.sh 
['item 1', 'item 2', 'item 3', 'item 4', 'item 5']
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/11$ python3
Python 3.8.10 (default, Nov 26 2021, 20:14:08) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> myvar = ['item 1', 'item 2', 'item 3', 'item 4', 'item 5']
>>> print (myvar)
['item 1', 'item 2', 'item 3', 'item 4', 'item 5']
>>> print (myvar[0])
item 1
>>> print (myvar[1])
item 2
```
### Dictionary
Whatever comes after the colon is treated as the value, any subsequent entries are treated as the same dictionary.
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/12$ cat test.yaml 
---
# Every YAML file should start with three dashes

example_key_1: example_value_1
example_key_2: example_value_2

# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/12$ ./show_yaml_python.sh 
{'example_key_1': 'example_value_1', 'example_key_2': 'example_value_2'}
```
### Indentation
is part of the YAML language and a two character indentation is a common practice for Ansible and other uses of YAML.
### Dictionary of Dictionary
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/17$ cat test.yaml 
---
# Every YAML file should start with three dashes

example_key_1:
  sub_example_key1: sub_example_value1

example_key_2:
  sub_example_key2: sub_example_value2

# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/17$ ./show_yaml_python.sh 
{'example_key_1': {'sub_example_key1': 'sub_example_value1'},
 'example_key_2': {'sub_example_key2': 'sub_example_value2'}}
```
### A dictionary key have a list of values
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/18$ cat test.yaml 
---
# Every YAML file should start with three dashes

example_1: 
  - item_1
  - item_2
  - item_3

example_2: 
  - item_4
  - item_5
  - item_6

# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/18$ ./show_yaml_python.sh 
{'example_1': ['item_1', 'item_2', 'item_3'],
 'example_2': ['item_4', 'item_5', 'item_6']}
```
### A list of dictionaries, consisting of a list of iteams
``` bash
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/19$ cat test.yaml 
---
# Every YAML file should start with three dashes

example_dictionary_1:
  - example_dictionary_2:
    - 1
    - 2
    - 3
  - example_dictionary_3:
    - 4
    - 5
    - 6
  - example_dictionary_4:
    - 7
    - 8
    - 9

# Every YAML file should end with three dots
...
ansible@ubuntu-c:~/diveintoansible/Ansible Playbooks, Introduction/YAML/19$ ./show_yaml_python.sh 
{'example_dictionary_1': [{'example_dictionary_2': [1, 2, 3]},
                          {'example_dictionary_3': [4, 5, 6]},
                          {'example_dictionary_4': [7, 8, 9]}]}
```

## Resources
Useful references
- [YAML Specification](http://yaml.org/spec/1.2/spec.html) 
- Other options for working with multi line input/output in YAML
https://stackoverflow/com/questions/3790454/in-yaml-how-do-i-break-a-string-over-multipe-lines 

### curly brackets vars
The curly brackets are part of the Jinja2 templating system for variables
``` bash
cat motd_playbook.yaml 
---
# YAML documents begin with the document separator ---

# The minus in YAML this indicates a list item.  The playbook contains a list 
# of plays, with each play being a dictionary
-

  # Hosts: where our play will run and options it will run with
  hosts: centos
  user: root
  gather_facts: False

  # Vars: variables that will apply to the play, on all target systems
  vars:
    motd: "Welcome to CentOS Linux - Ansible Rocks\n"

  # Tasks: the list of tasks that will be executed within the playbook
  tasks:
    - name: Configure a MOTD (message of the day)
      copy:
        content: "{{ motd }}"
        dest: /etc/motd

  # Handlers: the list of handlers that are executed as a notify key from a task

  # Roles: list of roles to be imported into the play

# Three dots indicate the end of a YAML document
...
```
### varible can pass by command line
`-e` or the `--extra-vars`
`ansible-playbook motd_playbook.yaml -e 'motd="testing the mod playbook\n"'`

### handlers
Handlers follow the same syntax as taks, are called from the task section through the use of the motified key within a task
``` bash
$ cat motd_playbook.yaml 
---
# YAML documents begin with the document separator ---

# The minus in YAML this indicates a list item.  The playbook contains a list 
# of plays, with each play being a dictionary
-

  # Hosts: where our play will run and options it will run with
  hosts: centos
  user: root
  gather_facts: False

  # Vars: variables that will apply to the play, on all target systems
  vars:
    motd: "Welcome to CentOS Linux - Ansible Rocks\n"

  # Tasks: the list of tasks that will be executed within the playbook
  tasks:
    - name: Configure a MOTD (message of the day)
      copy:
        content: "{{ motd }}"
        dest: /etc/motd
      notify: MOTD changed

  # Handlers: the list of handlers that are executed as a notify key from a task
  handlers:
    - name: MOTD changed
      debug:
        msg: The MOTD was changed

  # Roles: list of roles to be imported into the play

# Three dots indicate the end of a YAML document
...
```
### Resources
- Playbooks Keywords
https://docs.ansible.com/ansible/2.4/playbooks_keywords.html
