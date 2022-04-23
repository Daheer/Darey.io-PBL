<h2> Project 1: LAMP (Linux Apache2 MySQL PHP) Stack Implementation </h2>

<h4> Step 1: Installing Apache and Updating the Firewall </h4>

EC2 Instance Connection

<img src='EC2 Instance Connected.png'>

Commands

<ul>   
  
  <li> sudo apt update <br>
  <li> sudo apt install apache2 </li> 
  <br>
  <img src = 'Apache2 Installation.png'/> <br>
  <li> sudo systemctl status apache2 </li> <br>
  <img src = 'Apache2 Active.png'/> <br>
  <li> curl http://localhost:80 </li> <br>
  <img src = 'Apache2 Working.png'/> <br>
  <li> curl -s http://169.254.169.254/latest/meta-data/public-ipv4 </li> <br>
  <img src = 'Apache2 It Works.png'/> <br>
  
</ul>

<h4> Step 2: Installing MySQL </h4>

Commands

<ul>
  
  <li> sudo apt install mysql-server </li>
  <li> sudo mysql_secure_installation </li> <br>
  <img src = 'MySQL Secure Installation.png'/> <br>
  <li> sudo mysql </li> <br>
  <img src = 'MySQL.png'> 
  
</ul>

<h4> Step 3: Installing PHP </h4>

Commands

<ul>

  <li> sudo apt install php libapache2-mod-php php-mysql </li>
  <li> php -v </li> <br>
  <img src = 'PHP Installation.png'/>
  
</ul>

<h4> Step 4: Creating a Virtual Host for Apache to Serve a Website </h4>

Commands

<ul>
  
  <li> sudo mkdir /var/www/projectlamp </li>
  <li> sudo chown -R $USER:$USER /var/www/projectlamp </li>
  <li> sudo vi /etc/apache2/sites-available/projectlamp.conf </li>
  <li> sudo ls /etc/apache2/sites-available </li>
  <li> sudo a2ensite projectlamp </li>
  <li> sudo a2dissite 000-default </li>
  <li> sudo apache2ctl configtest </li>
  <li> sudo systemctl reload apache2 </li>
  <li> sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html </li> <br>
  <img src = 'Website.png'/>
  
</ul>

<h4> Step 5: Enabling PHP on the Website </h4>

Commands

<ul>
    
  <li> sudo vim /etc/apache2/mods-enabled/dir.conf </li>
  <li> sudo systemctl reload apache2 </li>
  <li> vim /var/www/projectlamp/index.php </li>
  <li> &lt?php <br>
phpinfo(); </li> <br>
  <img src = 'PHP Version Information.png'/>
  
</ul>


