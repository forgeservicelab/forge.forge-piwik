Name
=========

forge-piwik is a playbook that installs piwik analytics solution for apache web server. Piwik site configuration for apache is created and enables ssl connectios to piwik. The playbook also installs forge ssl certificates for the web servers.

Requirements
------------

An Ubuntu instance is provisioned and ready for ssh connections.

Variables
--------------

group_vars
	remote_user: ubuntu    # the user that has sudo rights used to install things
	ansible_ssh_user: ubuntu   # the user that has ssh access to the target machine
  

Dependencies
------------

inventory     - file that contains your server's ip address

ansible-piwik - role that creates default piwik installation
forge_ssl     - role that adds forge server certificats
piwik-ssl     - role that reconfigures piwik for ssl connections and disables default apahce http site conf


Example Usage
----------------

1. Create the virtual machine and have access to it as ubuntu user. Or change the group_vars to comply with the usernames you use.

2. Install dependendent roles

````
$ ansible-galaxy install -r requirements.yml
````

3. Check the inventory file and make sure that your server instance is correctly indicated there

````
$ ansible-playbook -i inventory
````

4. Go to your server https://[ip address]/piwik with the browser using https and then finalize piwik installation.

License
-------

BSD

Author Information
------------------

Pasi Kivikangas, pasi.kivikangas@digile.fi
