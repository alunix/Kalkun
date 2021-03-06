## Kalkun - Open Source Web-based SMS Management   
Kalkun is open source web-based SMS (Short Message Service) management, it use gammu-smsd (part of gammu family) as SMS gateway engine to deliver and retrieve messages from your phone/modem. 

Homepage : http://kalkun.sourceforge.net - Documentation : http://github.com/back2arie/Kalkun/wiki/

## Requirement
You need to install and configure this first:

* apache 2.x.x
* PHP 7.2.x / 5.x.x (with mysql/pgsql/pdo_sqlite, session, hash, json, mbstring extension)
* PHP-CLI   
* MySQL 5.x.x or PostgreSQL or SQLite3
* gammu-smsd, make sure it is already running and configured

## Installation:  

1. Extract to web root folder (eq: /var/www/html => Ubuntu)
2. Create database named kalkun (you can do it with mysql console or phpMyAdmin)
     ```
     # mysql > CREATE DATABASE kalkun;
     # mysql > quit
     ```

3. Edit database config (application/config/database.php)
   Change database value to 'kalkun', username and password is depend on your mysql configuration

4. Import gammu database schema (it's included on gammu source, eg. gammu/docs/sql/mysql.sql)  
    ```
    mysql kalkun - u username -p < gammu/docs/sql/mysql.sql
    ```

5. Configure daemon (to manage inbox and autoreply)
   -  Set path on gammu-smsd configuration at runonreceive directive, e.g:
      ```
      [smsd]
      runonreceive = /opt/lampp/htdocs/kalkun/scripts/daemon.sh
      ```
      or, if you using Windows:
      ```
      [smsd]
      runonreceive = C:\xampp\htdocs\kalkun\scripts\daemon.bat
      ```
   - set correct path (php-cli path and daemon.php path) on daemon.sh or daemon.bat 
   - make sure that the daemon script is executable
   - Change URI path in daemon.php, default is (http://localhost/kalkun)
	
6. Configure Kalkun
    - _There are 2 way configure_ 	
        - Graphic Install	
          Launch http://your-location/kalkun/index.php/install, and follow instruction there, or
        - Manual Install (import sql file media/db/mysql_kalkun.sql to kalkun database)
          ```
          mysql -u username -p kalkun < media/db/mysql_kalkun.sql
          ```

## IMPORTANT: 
  * After install finished, you need to remove install folder.
  * To improve security, it's higly recommended to change "encryption_key" on application/config/config.php
	
Open up your browser and go to http://your-location/kalkun

Default account (you can change it after you login) : 
`username = kalkun`
`password = kalkun`

Enjoy...:)
