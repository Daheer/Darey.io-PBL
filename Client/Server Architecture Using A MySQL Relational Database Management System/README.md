<h2> Project 5 (Client/Server Architecture Using A MySQL Relational Database Management System) </h2>

<h4> Step 1: Create and Configure Two Linux Based Virtual Servers </h4>

Commands

* sudo apt update
* sudo apt upgrade
* sudo apt install mysql-server
* sudo apt install mysql-client

<h4> Step 2: Create New User on the Remote Server with Necessary Privileges </h4>

* sudo mysql -h localhost
* CREATE USER 'user'@'%' IDENTIFIED BY 'default';
* GRANT ALL PRIVILEGES ON *.* TO 'user'@'%' WITH GRANT OPTION;
* FLUSH PRIVILEGES;
* EXIT;

    <img src = 'Created New User on Server.png'/>

<h4> Configure MySQL Server to Allow Connections From Remote Hosts </h4>

* sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf

    <img src = 'Changed Bind Address.png'/>

<h4> Connect Remotely to MySQL Server from MySQL Client </h4>

* sudo mysql -h 172.31.18.255 -p

    <img src = 'Connected to Remote Database.png'/>
