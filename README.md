### **Nextcloud installation on a Debian 10 server (fresh install)**
#### *Last updated: 04-07-2021*

******

1) Install Apache2:
   > $ sudo apt install apache2 libapache2-mod-php;

2) Install PHP:
   > $ sudo apt-get install -y php php-gd php-curl php-zip php-dom php-xml php-simplexml php-mbstring;

3) Install MySql-server and PHP Mysql support:
   > $ sudo apt install default-mysql-server php-mysql;

4) Log into MySql (no password is set, just press `ENTER` at the prompt):
   > $ sudo mysql -u root -p;

5) Create a database for the Nextcloud installation (replace 'Password123' with a password): 
   ```
    CREATE DATABASE nextclouddb;

    GRANT ALL ON nextclouddb.* TO 'nextcloud_user'@'localhost' IDENTIFIED BY 'Password123';

    FLUSH PRIVILEGES;

    EXIT;
   ```

6) Install `unzip`: 
   > $ sudo apt install unzip;

7) Download Nextcloud (At time of writing, latest v. is 21.0.0), and decompress: 
   > $ cd /tmp && wget https://download.nextcloud.com/server/releases/nextcloud-21.0.0.zip & unzip nextcloud-21.0.0.zip;

8) Move the `nextcloud` folder to the Apache2 webroot dir: 
   > $ sudo mv nextcloud /var/www/html

9) Go to webroot folder and change `nextcloud` dir ownership to `www-data`:
   > $ cd /var/www/html && sudo chown -R www-data:www-data nextcloud && sudo chmod -R 755 nextcloud;

10) Reboot the server (mandatory, post-PHP install): 
    > $ sudo systemctl reboot;

11) Install Nextcloud in the browser by navigating to `SERVER_IP/nextcloud/index.php`.
    
12) Create an admin account with a good username and strong password.

13) Enter database details matching what was created in `Step 5.`:
    - Database User: nextcloud_user
    - Password: Password123
    - Database Name: nextclouddb
    - Address: localhost

14) All done!  Step 13 may take several minutes, don't navigate away from the page! 
