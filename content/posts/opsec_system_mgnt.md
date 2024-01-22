---
title: "The OpSec Series - System Management"
date: 2024-01-22T22:06:28+01:00
author: "Valentijn Harmers"
draft: true
showtoc: false
description: "Desc Text."
categories: ["Technology"]
tags: ["opsec", "macos", "windows", "linux"]
---

Setting up systems can be a lengthy and boring process. It is easy to forget a step, execute it in the wrong order or use the wrong settings. I still remember the day when I had to reinstall the Operating System of my laptop on a yearly basis.

Microsoft Windows has a tendency to become slower over time. Installing all kinds of software like games and Integrated Development Environments (IDE’s) such as Visual Studio and Netbeans also didn’t help. Cleaning tools like CCleaner and Smart Defrag only got you so far. Sometimes the only thing left to do was to reinstall the OS and start fresh.

The most annoying part of this process was the installation of the needed applications and their configurations. I had to set the system up how I liked it. “Wouldn’t it be great if could just have a list of applications and settings I could feed to the computer and let it do the heavy lifting for me” I often thought. Little did I know that making these kind of lists would be a large part of my future job.

One of the big problems with manually setting up and managing systems is what I would call “system rot”. Changes, like adding and removing users or software or making configuration changes, accumulate over time. It is not always clear who made the change and what its purpose was.

It also makes it difficult to recreate a system because it is unclear which changes need to be applied to a base system in order to get the system you had. It’s like assembling a piece of IKEA furniture with no manual. You only get a picture of the already assembled product.

This becomes an especially large problem when a system is infected with malware. Trying to remove the malware may be an option but you never if there might be remnants left after the removal attempt. This can cause systems to get reinfected.

Your second option might be to bring the system back to an uninfected state by restoring a backup. I isn’t always clear went a system got infected however. I would be difficult to determine how far you have to go back to in oder to find a clean backup. It isn’t uncommon for attackers to have access on the systems of their victims for months or even years. So you might not have any clean backup to restore.

The solution to these problems is to keep track of all changes with a system configuration management tool. This allows you to detect and revert unauthorized changes to a system. There are multiple solutions out there but I have chosen Ansible for this blog post since it is the tool I have the most experience with.

## Managing Systems with Ansible
Ansible is an automation solution originally developed by Michael DeHaan and acquired by Red Hat in 2015. The tool is written in the Python programming language and heavily relies on YAML and Jinja2.

YAML stands for Yet Another Markup Language and is, as the name suggests, a markup language. Markup Languages can be used to write documents write and easy to read for both humans and machines. Other popular languages are XML and JSON. I created a shopping list application, which saves the shopping list in the JSON format, as part of my Python101 tutorial. You can check it out over [here](https://github.com/vharmers/python101/blob/master/lesson_10/storing_data.md).

Jinja2 is a templating engine written in Python. It allows for the use of variables and other functions in Ansible YAML files and system configuration files. Templating is great because it allows you to reuse parts of your code so you don’t have to repeat yourself.

There are some Ansible specific terms you need to know before we can proceed:

* **Inventory**; This is where information about all your Ansible managed systems is stored. The inventory essentially tells Ansible where your systems live. Systems (or hosts) can be organized in groups and configuration can be applied at either host or group level.
* **Task**; An action which is carried out on a system. A task could be anything. The creation of a directory or user account, the installation of a software package or the creation of a configuration file. Tasks rely on modules to actually execute the action.
* **Module**; Modules are be used by a tasks to do something, like copying a file. Ansible has a set of builtin modules, but there are also a lot of third party modules. Ansible’s builtin modules all have the `ansible.builtin` prefix. Examples in include `ansible.builtin.copy` and `ansible.builtin.user`.
* **Role**; A collection of related tasks. A role can be a collection of tasks for installing and configuring an Nginx Web Server for example. A system or group of systems can have multiple roles assigned to it.
* **Play(book)**; A play or playbook is essentially a file that defines which Roles should be executed on which systems or groups.

There are some other terms that are not mentioned above, but I will introduce these later on. Let’s first look at the smallest element in Ansible:

```yaml
- name: Ensure user John Doe exists
  ansible.builtin.user:
    name: john.doe
	groups:
      - global
      - accounting
      - emergency_response
```

The code block above shows the definition of a single task. Each task has a name and makes use of a module to achieve its intended goal. Here we make use of the `ansible.builtin.user` module in order to create a user called ‘john.doe’. We also ensure that John is a member of the Global, Accounting and Emergency Response groups. This allows him to access additional files and folders apart from his own private files.

We can expand this example by ensuring the groups exist before trying to make John a member of them:

```yaml
- name: Ensure the Global group exists
  ansible.builtin.group:
  	name: global

- name: Ensure the Accounting group exists
  ansible.builtin.group:
  	name: accounting

- name: Ensure the Emergency Response group exists
  ansible.builtin.group:
  	name: emergency_response

- name: Ensure user John Doe exists
  ansible.builtin.user:
    name: john.doe
	groups:
      - global
      - accounting
      - emergency_response
```

We now have 4 tasks. 3 for creating groups and 1 for creating a user. We can further optimize the tasks by using loops. This will allow us to merge the 3 group tasks into a single task:

```yaml
- name: Ensure groups exists
  ansible.builtin.group:
  	name: "{{ item }}"
  loop:
    - global
    - accounting
    - emergency_response

- name: Ensure user John Doe exists
  ansible.builtin.user:
    name: john.doe
	groups:
      - global
      - accounting
      - emergency_response
```

The new group task will execute the `ansible.builtin.group` command for each item in the loop list. The `{{ item }}` placeholder will be replaced with the name current item during a playbook execution. This optimisation safes us from having to create tasks for each group we want to create.

We now have two tasks we like to run on our systems let’s take a look at how we can put these tasks in a role.
## Role structure
An Ansible role starts with the following directory structure:

```text
vharmers.template/
├── LICENSE
├── README.md
├── defaults
│   └── main.yml
├── files
│   └── template.bash
├── handlers
│   └── main.yml
├── tasks
│   ├── configure.yml
│   ├── install.yml
│   ├── main.yml
│   └── validate.yml
└── templates
    ├── template.conf.j2
    └── template.service.j2
```

The figure above shows the directory structure of my own template role. I use this role as a template for creating new roles. The `README.md` and `LICENSE` files should be self-explanatory but from there on things start to get interesting:

* **Defaults;** This folder contains the default variables of this role. These variables can all be overridden in the inventory. I will explain more about variables and the inventory in later sections.
* **Files;** This is the location where you put the files you want to use in your role. These files can be anything. You will be able to refer to these files within your tasks. The files in this folder are usually just copied to the target host by using the `ansible.builtin.copy` module within a task.
* **Handlers;** Are special tasks that are triggered by other tasks and run after the normal tasks have been executed. Handlers are uses in scenarios where an action only has be taken when a normal task actually introduces a change on a system. Most popular use cases include the restarting of a service when its configuration file has changed.
* **Tasks;** This is where the magic happens. This folder contains the tasks that need to be executed for this role. You can put all of your tasks in a single file but since roles can include a lot of tasks, it is recommended to pull related tasks into separate files to keep things structured.
* **Templates;** This folder contains the Jinja2 templates used by the role. These templates can be used the create things like configuration files.

## Using variables and templates
Variables allow us to refer to a value by using a name. Think of it as a shortcut or a reference. A role contains a set of default variables. The values of these variables can by overridden from the inventory. It is easiest to explain by showing an example:

```yaml
defaults/main.yml
---
groups:
  - global
  - accounting
  - emergency_response

users:
  - john.doe
  - jane.doe

tasks/main.yml
---
- name: Ensure groups exists
  ansible.builtin.group:
  	name: "{{ item }}"
  loop: "{{ groups }}"

- name: Ensure users exists
  ansible.builtin.user:
    name: "{{ item }}"
	groups: "{{ groups }}"
  loop: "{{ users }}"
```

The example above shows the contents two files (`defaults/main.yml` and `tasks/main.yml`). `default/main.yml` defines two variables called `groups` and `users`. The groups variable holds a list of all the groups we need and the users variable hold a list of users who need an account on our systems.

These two variables can be used in the `tasks/main.yml` file to refer to the group and user lists.  If we want to add our users to a new group then we can simply add the group to the `groups` list. This saves us the trouble of having to add the new group at two locations.

Variables always need to be enclosed with four brackets (`{{ groups }}`). The brackets tell Ansible, or rather Jinja2, that `group` is a reference to a variable rather than a normal string. We also need to add quotes to indicate the contents have special meaning and need to be interpreted with Jinja2 which in turn will recognise the variable and replace it with whatever it points to.

Variables can also be used in templates. Templates are stored in the templates folder. All templates have the “.j2” file extension (j2 is shorthand for jinja2). Here is an example of a template file:

```jinja2
{% if length(groups) > 0 %}
This system has the following groups:
{% for group in groups %}
  - {{ group }}
{% endfor %}

{% endif %}
{% if length(users) > 0 %}
This system has the following users:
{% for user in users %}
  - {{ user }}
{% endfor %}

{% endif %}
```

The template contains some elements that are enclosed with brackets and procent signs (`{% ... %}`). These differ from the `{{ … }}` blocks that are used for printing the value of a given variable. The `{% ... %}` blocks are used for special instructions.

At first we check if the `group` variable contains any elements. We do this by using the `{% if length(groups) > 0 %}` statements which roughly translates to “continue if the length of the groups list is greater that zero”. Jinja2 will continue parsing the template if the statement is true. Otherwise it will skip directly to the `{% endif %}` block and continue from there.

 The next thing would be the `{% for group in groups %}` statement. This simply means: “repeat for every element in the groups variable”. This statement will first retrieve the first element from the `groups` list, store it in the temporal `group` variable and continue until it stumbles upon the `{% endfor %}` block.

It will then jump back the for statement where it will now take the second element in the list and writes its value to the `group` variable and continue again until it gets to the `{% endfor %}`. This loop is continued until all the elements in the `groups` list have had their turn.

Then we do the exact same thing for the users variable. Parsing this template with Jinja2 will give you the following result:

```plaintext
This system has the following groups:
  - global
  - accounting
  - emergency_response

This system has the following users:
  - john.doe
  - jane.doe

```

You can parse and copy templates to the targeted system by using the `anisble.builtin.template` module. Here is an example of a tasks using this module:

```yaml
- name: Ensure configuration is present
  ansible.builtin.template:
    src: template.conf.j2
    dest: "{{ template_config_dir }}/template.conf"
    owner: "{{ template_user }}"
    group: "{{ template_group }}"
    mode: 0644
  notify: Restart service
```

This task takes the template file `template.conf.j2` parses it and copies the result to a file called `template.conf` located in the configuration directory on the targeted system. It then ensures the file has the right owner, group and permissions. The last thing it does is notifying the `Restart service` handler tasks which in turn will restart the appropriate service when all other tasks have been executed.
## Inventory
Your inventory is simply a list of systems you want to manage with Ansible. You can put all your systems in the same inventory but you can also spread out your systems over multiple inventories. I personally prefer to have separate inventories for testing and production systems.

Inventories can be structured in either the INI or YAML format. Here is an example of in INI inventory:

```ini
files.example.com

[webservers]
web1.example.com
web2.example.com
web3.example.com

[databases]
db1.example.com
db2.example.com

[proxies]
proxy1.example.com
proxy2.example.com

[firewalls]
firewall1.example.com
firewall2.example.com
```

The example above shows five groups with each group having one to three members. There is also one system which doesn’t belong to any group. Here is an example of the same inventory but then formatted in YAML:

```yaml
ungrouped:
  hosts:
    - files.example.com
webservers:
  hosts:
    - web1.example.com
    - web2.example.com
    - web3.example.com
databases:
  hosts:
    - db1.example.com
    - db2.example.com
proxies:
  hosts:
    - proxy1.example.com
    - proxy2.example.com
firewalls:
  hosts:
    - firewall1.example.com
    - firewall2.example.com
```

You are free to choose which format to use. I would however advise you to choose and stick with one format.

Once you have your inventory you can define your playbook. Here is an example playbook:

```yaml
- hosts: all
  roles:
    - common

- hosts: webservers
  roles:
    - apache2

- hosts: databases
  roles:
    - mariadb

- hosts: proxies
  roles:
    - tinyproxy

- hosts: firewalls
  roles:
    - nftables
```

A playbook is simply the glue between the inventory and the roles. It defines which roles should be executed on which systems. The apache2 role is executed on all systems in the webservers group for example. The ‘all’ pattern is used to select all systems in the inventory so the ‘common’ role is executed on all systems.

The default variables for the systems in the inventory can be overridden in the playbook by adding a ‘vars’ section like this:

```yaml
- hosts: databases
  roles:
    - mariadb
  vars:
    mariadb_user: admin
    mariadb_password: password
```

Note that variable names are often prepended with the name of the role they belong to. This is because all roles share the same variable space. This means that roles will override each-others variables if they use the same variable names.

A more proper way to override variables is by putting the variables in separate files. You can make folders for each group and create a file called ‘main.yml’ in each folder. Then you can put the override variables in these main yaml files. You need to create the folders in the same directory where the inventory file is located and the names of these folders need to have the same name as the groups you want to override the variables for.

## Installing Ansible
As mentioned earlier, Ansible is written in Python. You therefore will need a Python interpreter installed. Most Linux distributions already come with Python version 3 preinstalled. macOS also has Python installed by default but it is the older version 2. It is recommended to install the newer version 3 through Homebrew:

```bash
brew install python3 python3-pip
```

Python comes with its own package manager called ‘pip’. You can use it to install Ansible:

```bash
pip3 install ansible
```

Some distributions also offer Ansible as a package. You can also install Ansible directly with Homebrew for example:

```bash
brew install ansible
```

It is hoverer recommended to stick with one strategy. Installing Ansible with the systems package manager as well as pip will end up confusing your system since the same application has been installed twice.

Ansible is also not available for the Windows Operating System although there is a Python interpreter available for Windows. The application will not run on Windows because it makes use of functions that are only available on Posix compliant systems like Linux and macOS. A solution to this problem is to run Ansible on top of Windows Subsystem for Linux or Cywin.
## Using Ansible Vault
As you can see the earlier code example, we define a `mariadb_user` and `mariadb_password` variable. It’s not the best idea to leave passwords in plaintext because inventory files are often kept in version control solutions such as Git. These solutions are not made with access control in mind. Anyone with access to the repository will be able to see the password and use it to login on the database.

A solution to this problem is to encrypt the password with Ansible Vault. This solution is builtin to Ansible and requires no additional software. Ansible Vault can encrypt whole files or strings of  text (inline).

Inline encryption is the easiest. Open up a command prompt and execute the following command:

```bash
ansible-vault encrypt_string --ask-vault-password --encrypt-vault-id default
```

The tool will prompt you for a vault password used to encrypt the string with and will then allow you to type the string to encrypt. Press *Crtl+D* when you are done typing the string. Ansible Vault will then print the encrypted multiline string. You can paste this string into your YAML file. Here is an example of what this looks like:

```yaml
- hosts: databases
  roles:
    - mariadb
  vars:
    mariadb_user: admin
    mariadb_password: !vault |
      $ANSIBLE_VAULT;1.1;AES256
      313764333530363435666238313764343063353461613332623538663134663561
      34363532303933393261623863663661310a613739316339346432613639383034
      363038396634633261343333316466643366336565373335663065656465323166
      61340a633039363737383934363439653932626466366665386362616363363639
      6439
```

As you can see, the value of the `mariadb_password` variable has been replaced with a Ansible Vault encryption block.

You might have noticed that apart from the `--ask-vault-password` option, we also need to supply the `--encrypt-vault-id` option with the value of `default`. Ansible Vault allows you to use multiple separate vaults in your inventory. You can for example have a “production” vault for all the production credentials and a “test” vault for all the test credentials. “default” is the name of the standard vault used by Ansible.

A similar process can be followed to encrypt a whole file:

```bash
ansible-vault create --ask-vault-password --encrypt-vault-id default vault.yml
```

You can edit your existing vault file by replacing ‘create’ with ‘edit’ in the command shown above.  It is recommended to use placeholder variables when working with vault files. I will show you the contents of a main and vault file to show you what I mean:

```yaml
main.yml
---
mariadb_address: localhost
mariadb_port: 3306
mariadb_user: admin
mariadb_password: "{{ vault_mariadb_password }}"

vault.yml (decrypted)
---
vault_mariadb_password: password
```

This way of working allows you to easily see which variables have been configured without the need to decrypt the `vault.yml` file. Note that the above example shows you the decrypted version of `vault.yml` the encrypted version should look something like this:

```plaintext
$ANSIBLE_VAULT;1.1;AES256
38396432316565653734316563373234653338616561663263343339373933616238373334333331
6663636437616538336663396564393731623966323037340a376363636438346564306536396539
35646637363039383733353132623062306361633937343561343238616338646637353233386434
3130386433346436340a623266653333373366653530343864333632663233313630613137366133
65633065303434356239643566666236613733316536646630643133646636373437376365346462
3331326361633337653934326361656136656239633230303533

```

Having to copy paste the vault password into the terminal window each time you need to use Ansible Vault can be quite the pain. It’s also not wise from a security perspective since you could paste the password into the wrong window by accident. A solution to this problem is to use a password script instead.

Ansible allows you to supply with a file path where it should read the password from. You can do this by using the `--vault-password-file` option instead of the `--ask-vault-password` option. Here is an example of how to do this:

```bash
echo 'password' > default
ansible-vault encrypt_string --vault-password-file default --encrypt-vault-id default
```

You can store the password in a plaintext file but Ansible can also work with script. You can easily create a script that prints the password like the following example:

```bash
#!/usr/bin/env bash

pass show infra/ansible/vault@default
```

This bash script loads the vault password form Pass. This solution is saver since the password is not saved in plaintext. Don’t forget to give the file execution permissions otherwise Ansible won’t be able to execute it and will interpreted it as a plaintext file.

## Using Pass with Ansible
You can also choose to pull credentials from an external source such as the Pass password manager. You can use this by using a lookup plugin. The pass lookup plugin is shipped with Ansible so there is no need to install any additional software.

Here is an example of how to use it:
```yaml
mariadb_user: admin
mariadb_password: "{{ lookup('pass', 'infra/production/admin@db1.example.com') }}"
```

You can use lookup plugins with the `lookup` function. The first argument of this function will always be the name of the plugin you wish to use. The rest of the arguments are passed to the plugin.

Accessing credentials like this can be useful if you want to have access to credentials from multiple tools. You can for example load the credentials into a Bash or Python script in order to connect to the database to do some maintenance work.
## Managing privileges
Making changes to an operating system such as Linux or Windows usually requires administrative privileges. You can tell Ansible for which tasks it should use admin privileges by using the become option. Here is an example of what I mean:

```yaml
- name: Ensure that the Python package is installed
  ansible.builtin.package:
    name: python3
    state: present
  become: yes
```

The `become: yes` option instructs Ansible to use admin privileges, also revered to as ‘sudo privileges’ in the Linux world, to install the python3 package since a regular user is not allowed to install packages on a system.

You will have to ensure that the user which is by Ansible actually has sudo privileges. This can usually be achieved by adding the user to a certain group. Using the sudo command requires the user password by default on many systems. You can supply this password to Ansible by including the `--ask-become-pass` switch into your playbook command.

## Running a playbook
I have now explained how to set everything up but you might wander how to actually execute an Ansible playbook run. You can execute a run with the following command:

```bash
ansible-playbook --inventory inventory.ini play.yml
```

Here we tell Ansible which inventory and playbook to use for execution. Your roles should be located in a folder called ‘roles’. There is no option to set the roles path from the commandline but you can set a custom role path by using the `ansible.cfg` configuration file.

To do this, simply create a new file called `ansible.cfg` in your inventory directory with the following content:
```plaintext
roles_path = $HOME/Documents/ansible-roles
```

Change the path value to any value you would like. You can configure far more things in the configuration file than you can with commandline options. You can generate a full configuration file by using the following command:

```bash
ansible-config init --disabled > ansible.cfg
```

Feel free to use this file as a starting point for your own custom configuration. Remove the semicolon in front of a particular option to make it active.
## Closing words
There is much more I can tell you about Ansible but I believe this is enough to get you started. This blog post will be the last post of the OpSec Series. It also acts as a bridge to my next series of blog posts which will focus more on Infrastructure As Code (IAC).

My goal with this new blog series is to give people a standardized and structured approach for deploying infrastructure in cloud and on-premise environments. I will mainly explain how IAC tools like Anisble, Terraform and Packer work and how they can be used effectively.

It has been about a year ago when I started this blog series and it has been an interesting journey. I often overestimated the time I needed to finish a blog post and always wanted them to be as complete as possible. Writing these blog posts has been a good tool to organize my knowledge and experiences. It is something that I want to continue to do.

I guess that’s all I wanted to say. Have a good day. See you at my blog post series (or not if IAC does not interest you).
