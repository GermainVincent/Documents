#### HOW TO INSTALL AN APACHE SERVER
-----------

1) Login into server :
* root@code-closet.com (or vps355203.ovh.net)

2) Install Apache with this two command : 
* apt-get update (récupère la dernière version)
* apt-get install apache2

3) Check if working by typing the IP adress or the adress on browser :
* http://code-closet.com or 51.255.51.212

4) Install MySQL :
* apt-get install mysql-server libapache2-mod-auth-mysql php5-mysql

5) Activate SQL :
* mysql_install_db

6) Run SQL setup script :
* /usr/bin/mysql_secure_installation

7) Install PHP :
* apt-get install php5 libapache2-mod-php5 php5-mcrypt

8) Add PHP to the directory index :
* /etc/apache2/mods-enabled/dir.conf

9) Adding PHP modules :
* apt-cache search php5- (Print a list of all available module)
* apt-get install "name of the module" (Install the selected module by its name)
<br/><br/>

#### HOW TO SETUP AN APACHE VIRTUAL HOST ON UBUNTU
--------------
1) Make sure we have installed an apache server and created a non root user profile

2) Create or use an existing domain name

3) Create directories to hold our website files :
* mkdir -p /var/www/example.com/public_html

4) Get permissions to modify the files of our website contained in the actual domain and subdomain :
* chown -R $USER:$USER /var/www/example.com/public_html<br/>
*$USER variable will take the value of the actual logged-in user*

5) Create or copy webpages in the correct directory :
* We can copy/paste files from our computer
* We can create new HTML files (index.html here) directly: nano /var/www/example.com/public_html/index.html
* We also can copy files from a virtual host to another one: cp /var/www/example.com/public_html/index.html /var/www/test.com/public_html/index.html
* With "nano" command we can enter and modify a file at any time

6) Create virtual host configuration files for all of our domain by copying the default configuration file into our virtual host (.conf) :
* cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/example.com.conf
* WARNING: While using Laravel or Symphony we have to load the .htaccess (hidden file. Use ls -la to show it) that is located in "public" folder to add the routing rules. To allow this we have to write this in the .conf file :<br/>
Directory /var/www/html/code-closet/public/	AllowOverride All	/Directory<br/>
*This will allow laravel to use the routing rules from .htaccess*

7) Modify the configuration file :
First open it => nano /etc/apache2/sites-available/example.com.conf 
Modify the server admin mail by an appropriate one:
Type: ServerAdmin admin@example.com
Then we have to enter the server name and server alias :
* ServerName example.com
* ServerAlias www.example.com
Finaly we have to set up the location of the root document for our domain:
DocumentRoot /var/www/example.com/public_html
* If needed we can copy this configuration file into another virtual host:
* cp /etc/apache2/sites-available/example.com.conf /etc/apache2/sites-available/test.com.conf
Save and close

8) Enable the virtual host :
* a2ensite example.com.conf

9) restart the server to make the changes works :
* service apache2 restart

10) Test it by writing its adress in the browser
<br/><br/>

<strong>NB:</strong>

How to get my server IP adress :
* ifconfig eth0

Restart the Apache server :
* service apache2 restart

Virtual host : 
* Apache breaks its functionality and components into individual units that can be customized and configured independently. The basic unit that describes an individual site or domain is called a virtual host.


	

	

