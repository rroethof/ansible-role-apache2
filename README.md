# Apache2 Webserver

[![Build Status](https://travis-ci.org/rroethof/ansible-role-apache2.svg?branch=master)](https://travis-ci.org/rroethof/ansible-role-apache2)

Basic feature list:

 * installs the apache2 webserver
 * creates virtual hosts based on the yml variables


## Requirements


## Role Variables

```yaml
webserver: apache2
webserver_vhosts:
  - servername: "vhost1.example.com"
    serveralias: "alias1.example.com"
    serveradmin: "admin@example.com"
    documentrootdir: "/var/www/vhost1.example.com"
    errorlog: "/var/log/httpd/vhost1.example.com"
    customlog: "/var/log/httpd/vhost1.example.com"
    directoryoptions: +Indexes
    allowfrom: 172.16.0.1/24
    denyfrom: all
    directoryindex: index.php
  - servername: "vhost2.example.com"
    configfile: "vhosts2.example.com.conf"
```


## Dependencies


## Example Playbook

```yaml
    - hosts: servers
      roles:
         - apache2
```

```bash
TASK: [apache2 | Include OS-specific variables.] ****************************** 
ok: [SUAPPL02]

TASK: [apache2 | Installeer de apache2 webserver (Debian)] ******************** 
skipping: [SUAPPL02]

TASK: [apache2 | Installeer de apache2 webserver (RedHat)] ******************** 
ok: [SUAPPL02] => (item=httpd)

TASK: [apache2 | Create web directories for each enabled VirtualHost] ********* 
changed: [SUAPPL02] => (item={'customlog': '/var/log/httpd/vhost1.example.com', 'serveradmin': 'admin@example.com', 'serveralias': 'alias1.example.com', 'servername': 'vhost1.example.com', 'errorlog': '/var/log/httpd/vhost1.example.com', 'documentrootdir': '/var/www/vhost1.example.com'})
changed: [SUAPPL02] => (item={'customlog': '/var/log/httpd/vhost2.example.com', 'serveradmin': 'admin@example.com', 'serveralias': 'alias2.example.com', 'servername': 'vhost2.example.com', 'errorlog': '/var/log/httpd/vhost2.example.com', 'documentrootdir': '/var/www/vhost2.example.com'})

TASK: [apache2 | Create a VirtualHost file for each enabled VirtualHost] ****** 
changed: [SUAPPL02] => (item={'customlog': '/var/log/httpd/vhost1.example.com', 'serveradmin': 'admin@example.com', 'serveralias': 'alias1.example.com', 'servername': 'vhost1.example.com', 'errorlog': '/var/log/httpd/vhost1.example.com', 'documentrootdir': '/var/www/vhost1.example.com'})
changed: [SUAPPL02] => (item={'customlog': '/var/log/httpd/vhost2.example.com', 'serveradmin': 'admin@example.com', 'serveralias': 'alias2.example.com', 'servername': 'vhost2.example.com', 'errorlog': '/var/log/httpd/vhost2.example.com', 'documentrootdir': '/var/www/vhost2.example.com'})

TASK: [apache2 | Ensure Apache is started and enabled on boot.] *************** 
ok: [SUAPPL02]
```


## License



## Author Information

This role was created in 2015 by Ronny Roethof for FDMedia, inspired by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
