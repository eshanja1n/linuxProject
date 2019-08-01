I am having trouble connecting to server on port 2200. I entered Port 2200 in my sshd_config file, but I keep getting a timeout error every time. Do you have any suggestions?

Also, whenever you go to the url, I keep getting the Apache default page. I've copied my ItemCatalog github repo, but how to I display the ItemCatalog instead of the Apache page?


**IP Address:** 54.244.8.32
**URL** http://54.244.8.32/

**Accessible SSH port:** 22





#Private Key: please set the permission on the file to :
$ chmod 600 

-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABFwAAAAdzc2gtcn
NhAAAAAwEAAQAAAQEA2WyTdnRkqWdcn8GDJ4XobSXB90u8fnTfHajCb7Q8GjXJRBdh2KF3
u7FN61Mtu/rRBglwPRcKZDclzLFgK0kWt75G/ht5YO+FUdKOofOq1XVZw/SDRkmtyPaQ+9
RgKgEzmnJQtV4YZHoATlo6dsugiwaeh7JweOk2Eu2tDpfVqNGJPio8h1DAEAA8mffzNPlI
7aNn4sbeZKuZcozd48sSx8eTNs1RmwGKynFdo9jhap3izmjDmeFyBv38f9a3Hh7s0c6owh
dGZOmlv2IG1xxETaTeGlcnTA2qcL8xWPXBDpRGIHK3nuMfPqxuzith4qjoXeI2y5YM24oD
fiXCzUbn5wAAA+DBHnrzwR568wAAAAdzc2gtcnNhAAABAQDZbJN2dGSpZ1yfwYMnhehtJc
H3S7x+dN8dqMJvtDwaNclEF2HYoXe7sU3rUy27+tEGCXA9FwpkNyXMsWArSRa3vkb+G3lg
74VR0o6h86rVdVnD9INGSa3I9pD71GAqATOaclC1XhhkegBOWjp2y6CLBp6HsnB46TYS7a
0Ol9Wo0Yk+KjyHUMAQADyZ9/M0+Ujto2fixt5kq5lyjN3jyxLHx5M2zVGbAYrKcV2j2OFq
neLOaMOZ4XIG/fx/1rceHuzRzqjCF0Zk6aW/YgbXHERNpN4aVydMDapwvzFY9cEOlEYgcr
ee4x8+rG7OK2HiqOhd4jbLlgzbigN+JcLNRufnAAAAAwEAAQAAAQBwcwZFYmdZchrmiSfy
/f+6y6do5iPD52Apr8l4Cmh3SdAhRlKVvtT1HvtktS1XJp6Kl8ET52G5eQg0uJw7Zt64A1
ImREFfkCGMsvCP9D0rjzjw7voiFSMrZ9KOXEWsE9kDjRIO626EMNENtP69yAztOmwtVG11
K3CLE5/Ih2C6oUhDUsw/GL0vpx8GtgQT9jzUN9NUDI9i8zPGEnjzLcICqjXy2oOtErbDwk
d6xtqXPK9QwQqEZStzcf1x3ryXzpNygWGm9ZUvnAKNjq5ixSSPb+8DX0pYeTzDP1FwT7Av
08FOKRz2bXuveBX78YKLGn16KKL9OzlFgYazH2zxfZURAAAAgFo2p+tRvT/3tGc/nSZzEb
68rdt1okonoSSa9bDPciZWHxuLE/f6acaWD4USidQD5B42E4joSNgOVpbaM0WVgeU7km3G
QlDXBwvqDjh8sxFfNUjUf4W5IqJnb5zbBBuujN52N59vGvLOMD+btKYyaypXgqDmC2nZA1
pAXSSe2Eb1AAAAgQD0B4r0U4CCOGJbY7nd3JYxJOhwEDxfedL6Uxp7eLgUbVH0zQtVeg6z
4q+jFLPhpRRRsUx681VuD6Gqnv038vGb1AKpMMf8by9aTEMllnsT2b9mGrMfRhLwUnulaG
GEK04Y+vappXPLC/nNKrUAOnu+2Wwg1p1uGjVnoe17uFo37wAAAIEA5BbuMj9U26GNSe6N
NwnGm/3GnDlKDXLhscqHj+k44lwW08uddLI3CMuMBPnRHZqwSRpEmSbiqWGzJ4vZh/Daf6
qsOQa5CJ6kp6ghqtLzzmBFR4Po1sI2O7ZDFppufEoDsjf+QVn+RWj/AkC+kwwVcTP+WeMh
R7/tXnGsJMkPl4kAAAAkbmlzaG1hamFpbkBOaXNobWFzLU1hY0Jvb2stUHJvLmxvY2FsAQ
IDBAUGBw==
-----END OPENSSH PRIVATE KEY-----

#if the private key does not work, try to ssh using the key in the file attatched and set the permissions to 
$ chmod 600

#Apps used to create:
- Apache
- Postgre
- Sqlalchemy
- Flask
- Virtual Host

1. created a new instance on amazon lightsail
2. clicked orange button to ssh into project. 
3. updated the installed packages
$ sudo apt-get update
$ sudo apt-get upgrade
4. Configured the Uncomplicated Firewall (UFW):

$ sudo ufw default allow outgoing
$ sudo ufw allow www
$ sudo ufw allow ntp
$ sudo ufw allow 2200/tcp
$ sudo ufw enable

5. Changed the SSH port from 22 to 2200
$ sudo vim /etc/ssh/sshd_config 
#changed the port from 22 to 2200 within the file
#the restarted ssh service using:
$ sudo service ssh restart

6. added new grader user:
$ sudo adduser grader
#set password to grader
#gave `Sudo` Access to grader and set NOPASSWD
$ sudo vim /etc/sudoers.d/grader
#Edit and following line to this file
grader ALL=(ALL) NOPASSWD:ALL
#Generated a keypair and push it to server.
# on local machine, generated a key pair:
$ssh-keygen -t rsa
#copied and pasted the key from local machine, usign vim editor:
$ vim .ssh/authorized_keys
#Changed permission of `.ssh` and `.ssh/authorized_keys`
$ chmod 700 .ssh
$ chmod 644 .ssh/authorized_keys
7. Changed timezone to UTC:
$ sudo timedatectl set-timezone UTC

8. Install and configure Apache to serve a Python mod_wsgi application.
$ sudo apt-get install apache2 libapache2-mod-wsgi
**Enabled mod_wsgi:**
$ sudo a2enmod wsgi

9. Installed and configured PostgreSQL:
$ sudo apt-get install libpq-dev python-dev
$ sudo apt-get install postgresql postgresql-contrib

10. Created new database user named **catalog** 
$ sudo su - postgres
$ psql

* Create a new database named *catalog*:    `# CREATE DATABASE catalog;`
* Create a new user named *catalog*:    `# CREATE USER catalog;`
* Set a password for catalog user:    `#  ALTER ROLE catalog with password 'password';`
* Grant permission to catalog user:    `# GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;`
* Exit from psql:    `# \q;`
* Return to grader using: `$ exit`

11. Installed python-pip, Flask and other dependencies.
`$ sudo apt-get install python-pip
$ sudo pip install Flask
$ sudo pip install sqlalchemy psycopg2 sqlalchemy_utils
$ sudo pip install httplib2 oauth2client requests

12. Changed the database connection to:
engine = create_engine('postgresql://catalog:password@localhost/catalog')

13. clone my git repo into project:
$ sudo mkdir /var/www/ItemCatalogFlaskApp
$ sudo mkdir /var/www/ItemCatalogFlaskApp/FlaskApp

* Made `grader` as ownner of that directory
$ sudo chown -R grader:grader /var/www/ItemCatalogFlaskApp
#cloned repo into /var/www/ItemCatalogFlaskApp/FlaskApp
$ sudo git clone https://github.com/eshanja1n/itemcatalog

14. Create the .wsgi file in *ItemCatalogFlaskApp*:
$ cd /var/www/ItemCatalogFlaskApp/
$ sudo vim ItemCatalogFlaskApp.wsgi
* Added the following lines of code to the `.wsgi file`
```python
#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/ItemCatalogFlaskApp")
from FlaskApp import app as application
```
15. Configuref and Enabled New Virtual Host:
$  sudo vim /etc/apache2/sites-available/000-default.conf
#added the following lines to the file
```xml
<VirtualHost *:80>
    ServerName 'test1'
    ServerAdmin nishmaj@gmail.com
    WSGIScriptAlias / /var/www/ItemCatalogFlaskApp/ItemCatalogFlaskApp.wsgi
    <Directory /var/www/ItemCatalogFlaskApp/FlaskApp>
        Order allow,deny
        Allow from all
    </Directory>
    Alias /static /var/www/ItemCatalogFlaskApp/FlaskApp/static
    <Directory /var/www/ItemCatalogFlaskApp/FlaskApp/static/>
        Order allow,deny
        Allow from all
    </Directory>
    ErrorLog /home/grader/serverErrors/serverError.log
    LogLevel warn
    CustomLog /home/grader/serverErrors/access.log combined
</VirtualHost>
```

16. enabled virtual host:
$ sudo a2ensite 000-default

17. 7. Restarted Apache to run the app on sever:
$ sudo apt-get purge apache2
$ sudo apt-get install apache2


#Whenever I try to ssh to the server from my terminal or another computer, 
#I am never able to connect. I included a screenshot of the error I recieve
#when I try to do this. 
