# Project 4 Setup WordPress Website Using LAMP Stack

Setting up a WordPress website using the LAMP stack (Linux, Apache, MySQL, PHP) is a powerful way to create a robust and scalable web presence. This project will guide you through each step of the process, from setting up your server environment to installing WordPress and configuring it for optimal performance. Whether you're a seasoned developer or a beginner, this tutorial will provide you with the knowledge and skills needed to deploy a fully functional WordPress site. By the end of this guide, you'll have a solid understanding of how to leverage the LAMP stack to build and manage your own WordPress website, ensuring a secure, efficient, and customizable platform for your content.

**Key Features:**

- Step-by-step instructions for installing and configuring LAMP components.
- Secure database creation for your WordPress website.
- User-friendly guide for completing the WordPress installation process.

**Benefits:**

- Gain independence by managing your own WordPress website.
- Understand the core technologies behind WordPress.
- Customize your website to your exact needs.
- Embrace the flexibility and power of WordPress.

## Introduction

Before we begin, let's review the tools we'll be using throughout this project.

### Linux

Linux is the cornerstone of the LAMP stack, serving as the operating system that underpins the entire infrastructure. As an open-source and highly customizable platform, Linux provides a stable and secure environment for hosting web applications. Its efficiency in handling processes and resources makes it an ideal choice for web servers. In a LAMP stack, Linux coordinates the interaction between Apache (the web server), MySQL (the database), and PHP (the scripting language), ensuring seamless operation and communication between these components. This foundation allows for high performance, flexibility, and scalability, making Linux a crucial element in the successful deployment and management of a LAMP-based WordPress website.

### Apache

Apache is a critical component of the LAMP stack, acting as the web server that handles client requests and serves web content. As an open-source and widely used web server software, Apache is known for its reliability, security, and flexibility. In a LAMP stack, Apache processes incoming HTTP requests, fetching and delivering web pages to users' browsers. It also supports various modules that extend its functionality, such as URL redirection, authentication, and load balancing. By efficiently managing web traffic and providing a stable platform for running web applications, Apache ensures that your WordPress website runs smoothly and can handle a large number of concurrent users.

### MySQL

MySQL is the database management system within the LAMP stack, responsible for storing and managing the data that powers your web applications. As an open-source relational database, MySQL offers robust performance, scalability, and security. In the context of a LAMP stack, MySQL works closely with PHP to handle data operations such as storing user information, retrieving content, and managing transactions. For a WordPress website, MySQL stores all the content, user data, settings, and other essential information, allowing for dynamic content generation and efficient data retrieval. By ensuring data integrity and providing powerful querying capabilities, MySQL plays a crucial role in maintaining the functionality and performance of a WordPress site on the LAMP stack.

### PHP

PHP is the scripting language in the LAMP stack, responsible for generating dynamic web content. As a server-side language, PHP processes code on the web server to create HTML content that is then sent to the user's browser. In the LAMP stack, PHP works in tandem with Apache to handle web requests and interact with the MySQL database to retrieve and manipulate data. For a WordPress website, PHP executes the core logic that powers the site, managing everything from user authentication to content management and plugin functionality. By seamlessly integrating with Apache and MySQL, PHP ensures that your WordPress site is dynamic, interactive, and capable of delivering a rich user experience.

---
## Project 4

|S/N | Project Tasks                                                       |
|----|---------------------------------------------------------------------|
| 1  |Deploy an Ubuntu Server                                              |
| 2  |Set up your LAMP stack on the server                                 |
| 3  |Configure the wordpress Application                                  |
| 4  |Map the IP address to the DNS A record                               |
| 5  |Validate the WordPress website setup by accessing the web address.   |

## Key Concepts Covered in this project:

- AWS (EC2 and Route 53)
- Linux(Ubuntu)
- Apache
- MySQL
- PHP
- Wordpress
- DNS
- SSL (certbot)
- OpenSSL command

## Checklist

- [x] Task 1: Deploy an Ubuntu Server
- [x] Task 2: Set up your LAMP stack on the server
- [x] Task 3: Configure the wordpress Application
- [x] Task 4: Map the IP address to the DNS A record
- [x] Task 5: Validate the WordPress website setup by accessing the web address.

## Documentation

Please reference [**Project1**](https://github.com/StrangeJay/devops-beginner-bootcamp/blob/main/project1/project1.md) for guidance on spinning up an Ubuntu server. and confirm the server is up and running

![1](img/1.png)

- Set an inbound rule for MYSQL in your security group. Click on **Security①** and select the **Security group②**.

![2](img/2.png)

-Click on  **Edit Inbound rule**  and then click on **Add rule**

![3](img/3.png) ![4](img/4.png)

- Click on **Custom TCP** and select **MySQL/Aurora**.

![5](img/5.png)

- Enter the **IP address①** you want to allow access and click **Save rules②**.

![6](img/6.png)

> [!NOTE]
You can choose 0.0.0.0/0 to permit access from anywhere, but for added security, restrict access to MySQL exclusively to your Web Server’s IP address. In the Inbound Rule configuration, specify the source as /32

- Open your **terminal**, cd into the folder where your keypair is located and connect to your Ubuntu server via SSH.

![7](img/7.png)

### Install Apache WEB Server on your Ubuntu Machine

- To install Apache, run the following commands in your terminal.

**`sudo apt update`** and **`sudo apt upgrade`**

![8](img/8.png)

**`sudo apt install apache2`**

![9](img/9.png)

- To enable Apache to start on boot, execute **`sudo systemctl enable apache2`①**, and then verify its status with the **`sudo systemctl status apache2`②** command.

![10](img/10.png)

- Now, let's check if our server is running and accessible both locally and from the Internet by executing the following command: **`curl http://localhost:80`**. it should show a default html file

![11](img/11.png)

*Now, it's time to test how our Apache HTTP server responds to requests from the Internet.*

- Copy your **public IPv4 address** from your EC2 dashboard.

![12](img/12.png)

- Open a web browser of your choice and try accessing the following URL: **`http://<Public-IP-Address>:80`**

- If the installation was successful, you should see this page.

![13](img/13.png)

### Install MYSQL

- To install this software using 'apt', run the command **`sudo apt install mysql-server`**. When prompted, confirm the installation by typing 'Y' and then pressing ENTER.

![14](img/14.png)

- After the installation is complete, log in to the MySQL console by typing: **`sudo mysql`**.

> [!NOTE]
It's recommended that you run a security script included with MySQL to enhance security. Before running the script, set a password for the root user using the default authentication method **mysql_native_password**. you can choose any password you prefer.

- Run the following command to set the password for the root user with the MySQL native password authentication method: **`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'pass';`**. Exit the MySQL shell when you're done by typing **`exit`**.

- Start the interactive script by running: **`sudo mysql_secure_installation`①**. Answer **y**② for yes, or any other key to continue without enabling specific options.

![15](img/15.png)

- Set your **password validation policy level**.Type 0 for LOW password policy level

> [!NOTE]
the password validation policy level was set to 0 because I don't require much security, as I will be terminating all resources immediately after this project. However, on the job, it's advised to use the strongest level, which is 2.

- Enable MySQL to start on boot by executing **`sudo systemctl enable mysql`①**, and then confirm its status with the **`sudo systemctl status mysql`②** command.

![16](img/16.png)

### Install PHP

- Install PHP along with required extensions by running the following script: **`sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip`**.

![17](img/17.png)

**`sudo apt install php libapache2-mod-php php-mysql`**

![18](img/18.png)

- Confirm the downloaded PHP version by running **`php -v`**.

![19](img/19.png)

### Creating A Virtual Host For Your Website Using Apache
- Create the directory for Projectlamp using the 'mkdir' command as follows:
**`sudo mkdir /var/www/projectlamp`①** and assign ownership of the directory to our current system user using:
**`sudo chown -R $USER:$USER /var/www/projectlamp`②**.

![20](img/20.png)

- Create and open a new configuration file in Apache's sites-available directory using your preferred command-line editor:
**`sudo vi /etc/apache2/sites-available/projectlamp.conf`**.

- Creating this will produce a new blank file. Paste the configuration text provided below into it:

```
<VirtualHost *:80>

ServerName projectlamp

ServerAlias www.projectlamp

ServerAdmin webmaster@localhost

DocumentRoot /var/www/projectlamp

ErrorLog ${APACHE_LOG_DIR}/error.log

CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```
![21](img/21.png)

- Save your changes by pressing the **`Esc`** key, then type **`:wq`** and press **`Enter`**.

![22](img/22.png)

- Run the ls command **`sudo ls /etc/apache2/sites-available`①** to show the **new file②** in the sites-available directory. you will see the projectlamp.conf file just created

![23](img/23.png)

- We can now enable the new virtual host using the a2ensite command: **`sudo a2ensite projectlamp`**.

- To disable Apache's default website, use the a2dissite command. Type: **`sudo a2dissite 000-default`**.

![24](img/24.PNG)

- To ensure your configuration file doesn’t contain syntax errors, run: **`sudo apache2ctl configtest`**. You should see **"Syntax OK"** in the output if your configuration is correct.

![25](img/25.PNG)

- Finally run: **`sudo systemctl reload apache2`**. This will reload Apache for the changes to take effect.

> [!NOTE]
Our new website is now active, but the web root **`/var/www/projectlamp`** is still empty. Let's create an **`index.html`** file in that location to test that the virtual host works as expected.

- To create the **index.html** file with the content **"Hello LAMP from Bruba"** in the /var/www/projectlamp directory, use the following command: **`sudo echo 'Hello LAMP from Bruba' > /var/www/projectlamp/index.html`**.

![26](img/26.png)

- Now, let's open our web browser and try to access our website using the IP address:

**`http://<EC2-Public-IP-Address>:80`**

> [!NOTE]
Replace **`<EC2-Public-IP-Address>`** with your actual EC2 instance's public IP address.

![27](img/27.png)

- Remove the index.html file by running the following command: **`sudo rm /var/www/projectlamp/index.html `**

### Enable PHP On The Website

**First**, prioritize php over html

With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. To change the precedence of index files (such as index.php over index.html) in Apache, you'll need to edit the dir.conf file. Here’s how you can do it:

- Edit the dir.conf file using a text editor (such as nano or vi): **`sudo nano /etc/apache2/mods-enabled/dir.conf`**

- Look for the DirectoryIndex directive within this file. It typically looks like this:

```
<IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>
```

- To prioritize **index.php** over **index.html**, move **index.php** to the beginning of the list, like this:

```
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
![28](img/28.png)

exit **(ctrl+x)** and save the changes when prompted by pressing **Y** and then **Enter**

- finally, reload APache2 for the changes to take effect:

![29](img/29.PNG)
Now, Apache will prioritize index.php over index.html when both files exist in the same directory.

**Second**, create a new file named index.php
- To create a new file named index.php inside your custom web root folder (/var/www/projectlamp), you can use the following command to open it in the nano text editor: **`nano /var/www/projectlamp/index.php`**.

- This will create a new file. Copy and paste the following PHP code into the new file:

```
<?php

phpinfo();
```
![30](img/30.png)

- Once you've saved and closed the file, go back to your web browser and refresh the page. You should see something like this:

![31](img/31.PNG)

> [!NOTE]
This page provides information about your server from the perspective of PHP. It is useful for debugging and to ensure that your settings are being applied correctly.

If you can see this page in your browser, then congratulations🎉 your PHP installation is working as expected.
After verifying the relevant information about your PHP server through that page, it's recommended to remove the file you created, as it contains sensitive information about your PHP environment and your Ubuntu server. You can use the rm command to do so:
**`sudo rm /var/www/projectlamp/index.php`**.

You can always recreate this page if you need to access the information again later.

---

### Install Wordpress

After setting up our LAMP environment, we can start installing WordPress. First, we'll download the WordPress installation files and place them in the default web server root directory: **/var/www/html**.

- Navigate to the directory using the cd command **`cd /var/www/html`**, and then download the WordPress installation files using the following command: **`sudo wget -c http://wordpress.org/latest.tar.gz`**

![32](img/32.PNG)

- Extract the files from the downloaded WordPress archive using the command: **`sudo tar -xzvf latest.tar.gz`**

- Run the command **`ls -l`** to confirm the existence of the **wordpress** directory in the current location (`/var/www/html`).

![33](img/33.PNG)

> [!NOTE]
The files must be owned by the user of your web server. Identify the web server's user and assign the appropriate permissions accordingly. The user **`www-data`** is widely adopted as the default user for web server processes, especially on Ubuntu and Debian systems. This user oversees the operation of web server software (like Apache or Nginx) and manages incoming web requests. However, for verification and for tasks involving services that may not have a predefined user, checking the user of the web server is advisable.

- Check the user running your web server with the command: **`ps aux | grep apache | grep -v grep`**.
*This command filters processes related to Apache (apache2 on Ubuntu) and displays information about the user running those processes.*

![34](img/34.png)

- Grant ownership of the WordPress directory and its files to the web server user **(www-data)** by running the command: **`sudo chown -R www-data:www-data /var/www/html/wordpress`**.

![35](img/35.png)

### Create a Database For Wordpress

- Access your MySQL root account with the following command: **`sudo mysql -u root -p`**. Enter the **password** you set earlier when prompted.
![36](img/36.PNG)

- To create a separate database named wp_db for WordPress to manage, execute the following command in the MySQL prompt: **`CREATE DATABASE wp_db;`**.

![37](img/37.PNG)

> [!NOTE]
This command allows you to create a new database (**wp_db**) within your MySQL environment. Feel free to name it as you prefer.

- To access the new database, you can create a MySQL user account with a strong password using the following command:

**`CREATE USER bruba@localhost IDENTIFIED BY 'wp-sequel';`**

![38](img/38.PNG)

*feel free to Replace 'wp-sequel' with your preferred strong password for the MySQL user account.*

- To grant your created user (bruba@localhost) all privileges needed to work with the wp_db database in MySQL, use the following commands:

```
GRANT ALL PRIVILEGES ON wp_db.* TO bruba@localhost;
FLUSH PRIVILEGES;
```

![39](img/39.PNG)

> [!NOTE]
This grants all privileges **(ALL PRIVILEGES)** on all tables within the wp_db database **(`wp_db.*`)** to the user jay when accessing from localhost. The FLUSH PRIVILEGES command ensures that MySQL implements the changes immediately. Adjust the database name **(wp_db)** and username **(bruba)** as per your setup.

- Type **`exit`** to exit the MySQL shell.

- Grant executable permissions recursively (-R) to the wordpress folder using the following command: **`sudo chmod -R 777 wordpress/`**

> [!NOTE]
This command sets read (r), write (w), and execute (x) permissions for the owner, group, and others on all files and directories within the wordpress folder. Using 777 permissions is quite permissive and may not be necessary for all files and folders; consider adjusting permissions based on security requirements.

- Change into the WordPress directory by running the command: **`cd wordpress`**.
![40](img/40.PNG)

### Configure Wordpress

Once you've established a database for WordPress, the next crucial step is setting up and configuring WordPress itself. To begin, you'll need to create a configuration file tailored for WordPress.

- Rename the sample WordPress configuration file with the command: **`mv wp-config-sample.php wp-config.php`**.

- Edit the **`wp-config.php`** file using the command: **`sudo nano wp-config.php`**.

![41](img/41.png)

- Update the database settings in the **`wp-config.php`** file by replacing placeholders like **database_name_here**, **username_here**, and **password_here** with your actual database details.
![42](img/42.png)

- Modify the configuration file projectlamp.conf: **`sudo nano /etc/apache2/sites-available/projectlamp.conf`** to update the document root to the directory where your WordPress installation is located.

![43](img/43.PNG)

- replace **`/var/www/projectlamp`** document root to **`/var/www/html`** directory in your editor, save the changes and exit.

![44](img/44.PNG)

- Reload Apache for the changes to take effect: **`sudo systemctl reload apache2`**.

- Once you've completed these steps, you can access your WordPress page to complete the installation. Open your web browser and go to **`http://<EC2 IP>/wordpress/`**. This will lead you to the WordPress setup wizard where you can finalize the installation process.

> [!NOTE]
Replace **<EC2 IP>** with the IP address of your EC2 instance when accessing your WordPress page.

- Select your preferred language and then click on **Continue** to proceed.

![45](img/45.PNG)

- Enter the required information and click on **Install WordPress** once you have finished.

  - **Site Title①:** Enter the name of your WordPress website. It's recommended to use your domain name for better optimization.
  - **Username②:** Choose a username for logging into WordPress.
  - **Password③:** Set a secure password to protect your WordPress account.
  - **Your email④:** Provide your email address to receive updates and notifications.
  - **Search engine visibility:** You can leave this box unchecked to prevent search engines from indexing your site until it's ready.

![46](img/46.PNG)

- WordPress has been successfully installed. You can now log in to your admin dashboard using the previously set up information by clicking the **Log In** button.
- Enter your username and password, then click **Log In** to access your WordPress admin dashboard.
- Once you successfully log in, you will be greeted by the WordPress dashboard page.

![47](img/47.png)

### Create An A Record

To make your website accessible via your domain name rather than the IP address, you'll need to set up a DNS record. I did this by buying my domain from Namecheap and then moving hosting to AWS Route 53, where I set up an A record.

> [!NOTE]
Visit [**Project1**](https://github.com/StrangeJay/devops-beginner-bootcamp/blob/main/project1/project1.md) for instructions on how to create a hosted zone.

- Point your domain's DNS records to the IP addresses of your Apache load balancer server.

- In route 53, click on **Create record**.

- Paste your **IP address➀** and then click on **Create records➁** to create the root domain.
![48](img/48.png)

- Click on **Create record** again, to create the record for your sub domain in this case www.domain name.

- To update your Apache configuration file in the sites-available directory to point to your domain name, use the command: **`sudo nano /etc/apache2/sites-available/projectlamp.conf`**.

> [!NOTE]
This command opens the **`projectlamp.conf`** file in the nano text editor with superuser privileges **(`sudo`)**. Within the editor, adjust the necessary details to reflect your domain name configuration.

- Ensure that the server settings in your Apache configuration point to your domain name, and that the document root accurately points to your WordPress directory. Once you've made these adjustments, save the changes and exit the editor.

```
<VirtualHost *:80>
    ServerName <Your root domain name>
    ServerAlias <Your sub domain name>
    ServerAdmin webmaster@<Your root domain name>

    DocumentRoot /var/www/html/wordpress

    <Directory /var/www/html/wordpress>
        Options Indexes FollowSymLinks
       # AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

```
![49](img/49.png)

> [!NOTE]
The new configuration defines how Apache should handle requests for your domain, and its subdomain. With this configuration: Apache will handle requests for **bruba.eu** and **www.bruba.eu**. Files will be served from the **`/var/www/html/wordpress`** directory. Directory listings and symbolic links are allowed. The directory can be accessed by any client.
Error logs will be written to **`/var/log/apache2/error.log`**. Access logs will be written to **`/var/log/apache2/access.log`** in the combined log format.

- To update your **`wp-config.php`** file with DNS settings, use the following command: **`sudo nano wp-config.php`** and add these lines to the file:

```
/** MY DNS SETTINGS */
define('WP_HOME', 'http://<domain name>');

define('WP_SITEURL', 'http://<domain name>');
```

Replace **`http://<domain name>`** with your actual domain name. Save the changes and exit the editor.

![50](img/50.png)

- Reload your Apache server to apply the changes with the command: **`sudo systemctl reload apache2`**, After reloading, visit your website at **`http://<domain name>`** to view your WordPress site. Replace **<domain name>** with your actual domain name.
![51](img/51.png)

- To log in to your WordPress admin portal, visit **`http://<domain name>/wp-admin`**, Enter your **username①** and **password②**, then click on **log In③**. *Replace **<domain name>** with your actual domain name.*

> [!NOTE]
My domain name is **bruba.eu**, so i'll visit **`http://bruba.eu/wp-admin`**.

![52](img/52.png)

- Now that your WordPress site is successfully configured to use your domain name, the next step is to secure it by requesting an SSL/TLS certificate.

### Install certbot and Request For an SSL/TLS Certificate

- Install certbot by executing the following commands:
`sudo apt update`
`sudo apt install certbot python3-certbot-apache`

![53](img/53.png)

- Run the command **`sudo certbot --apache`** to request your SSL/TLS certificate. Follow the instructions provided by Certbot to select the domain name for which you want to enable HTTPS.

![54](img/54.png)

- You should receive a message confirming that the certificate has been successfully obtained.

- Visit your website to confirm, and you'll notice that the **"not secure"** warning no longer appears, indicating that your site is now secure with HTTPS.

![55](img/55.png)
![56](img/56.png)

---
---

#### End