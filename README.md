Name
=========

forge-piwik is a playbook that installs piwik analytics solution for apache web server. Piwik site configuration for apache is created and enables ssl connectios to piwik. The playbook also installs ssl server certificates for apache.

Requirements
------------

An Ubuntu instance is provisioned and ready for ssh connections and ability to sudo.

Variables
--------------

--- group_vars/all.yml

````
apache:
  allow_ip: "83.150.108.249" # Allow http connections from
  sslcert: '/etc/ssl/certs/ssl-cert-snakeoil.pem'
  sslkey: '/etc/ssl/private/ssl-cert-snakeoil.key'
  # sslchain: '/etc/ssl/forgeservicela1b.fi.crt.chain'
````

Note! There is corresponding yml file for each target e.g. development, testing, production

Dependencies
------------

inventory     - file that contains your targets machines ip address and usernames
roles/ansible-piwik - role that creates default piwik installation
roles/forge_ssl     - role that adds forge server certificats
roles/piwik-ssl     - role that reconfigures piwik for ssl connections and disables default apache http site conf


Example Usage
----------------

1. Create the virtual machine and have access to it as ubuntu user. If you have ssh access to targets with different username then modify the inventory file accordingly.

2. Install dependendcies

````
$ ansible-galaxy install -r requirements.yml
````

3. Check the inventory file and make sure that your server instance is correctly indicated there. Also, have the server certificate corresponding key file in ./forgeservicelab.fi.key. Check that the name and location of your server certificates is correct in ./group_vars/all.yml (and corresponding target machines conf files). Set the allow_ip variable so that apache can be configured to allow connections to piwik from this address.

````
$ ansible-playbook -i inventory site.yml -e "targets=all"         or
$ ansible-playbook -i inventory site.yml -e "targets=development" or 
$ ansible-playbook -i inventory site.yml -e "targets=production"
````

4. Go to your server https://[ip address]/piwik with the browserand then finalize piwik installation. Please note! You can only access piwik from your defined allow_ip address

License
-------

MIT

Author Information
------------------

Pasi Kivikangas, pasi.kivikangas@digile.fi
