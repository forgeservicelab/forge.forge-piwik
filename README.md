Name
=========

forge-piwik is a playbook that installs piwik analytics solution for apache web server. Piwik site configuration for apache is created and enables ssl connectios to piwik. The playbook also installs forge ssl certificates for the web servers.

Requirements
------------

An Ubuntu instance is provisioned and ready for ssh connections.

Variables
--------------

--- group_vars
remote_user: ubuntu        - the user that has sudo rights used to install things
ansible_ssh_user: ubuntu   - the user that has ssh access to the target machine
sslcert: '/etc/ssl/forgeservicelab.fi.crt'
sslchain: '/etc/ssl/forgeservicelab.fi.crt.chain'
sslkey: '/etc/ssl/forgeservicelab.fi.key'

--- extra command line parameter for the playbook
ip_range - defines the IP range where the web browser access to piwik is allowed from

Dependencies
------------

inventory     - file that contains your server's ip address
roles/ansible-piwik - role that creates default piwik installation
roles/forge_ssl     - role that adds forge server certificats
roles/piwik-ssl     - role that reconfigures piwik for ssl connections and disables default apahce http site conf


Example Usage
----------------

1. Create the virtual machine and have access to it as ubuntu user. Or change the group_vars to comply with the usernames you use.

2. Install dependendent roles

````
$ ansible-galaxy install -r requirements.yml
````

3. Check the inventory file and make sure that your server instance is correctly indicated there. Also, put the server certificate corresponding forgeservicelab.fi.key into ./roles/forge_ssl/files/forgeservicelab.fi.key and check the group_vars/all.yml has information about the certificate files. Set the ip_range extra variable to be the address where you want to have access to piwik from

````
$ ansible-playbook -i inventory site.yml --extra-vars "ip_range=83.150.108.249"
````

4. Go to your server https://[ip address]/piwik with the browserand then finalize piwik installation. Please note! You can only access piwik from your defined ip_range address

License
-------

BSD

Author Information
------------------

Pasi Kivikangas, pasi.kivikangas@digile.fi
