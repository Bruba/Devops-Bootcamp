# Setup Multiple Static Websites on a Single Server Using Nginx Virtual Hosts

In this project, you will learn the concept of subdomains and hosting multiple websites on a single server using Nginx Virtual Host configuration.

## Documentation

Please reference [**Project1**](https://github.com/StrangeJay/devops-beginner-bootcamp/blob/main/project1/project1.md) for guidance on spinning up an Ubuntu server, as well as creating and associating an elastic IP address with your server, among other tasks.

- Spin up your ubuntu server, create an elastic IP and associate it to your instance.

### Install Nginx and Setup Your Website

- Execute the following commands.

`sudo apt update`

`sudo apt upgrade`

`sudo apt install nginx`

- Start your Nginx server by running the `sudo systemctl start nginx` command, enable it to start on boot by executing `sudo systemctl enable nginx`, and then confirm if it's running with the `sudo systemctl status nginx` command.

![1](img/1.png)

- Visit your instances IP address in a web browser to view the default Nginx startup page.

![2](img/2.png)

- Download your website template from your preferred website by navigating to the website, locating the template you want.

- Right click and select **Inspect** from the drop down menu.

- Click on the **Network** tab and then click **Download** button.

- Right click on the website name, select **Copy** and click on **Copy link address**.

- for this project, i downloaded the cafe and gymso template from toolplate

- To install the unzip tool, run the following command: **`sudo apt install unzip`**.

- Execute the command to download and unzip your website files `sudo curl -o /var/www/html/2126_antique_cafe.zip https://www.tooplate.com/zip-templates/2126_antique_cafe.zip && sudo unzip -d /var/www/html/ /var/www/html/2126_antique_cafe.zip && sudo rm -f /var/www/html/2126_antique_cafe.zip`.

![3](img/3.png)
---

**Here's an explanation of the command:**

The command **`sudo curl -o /var/www/html/2098_health.zip https://www.tooplate.com/zip-templates/2098_health.zip && sudo unzip -d /var/www/html/ /var/www/html/2098_health.zip && sudo rm -f /var/www/html/2098_health.zip`** performs a series of actions to download, unzip, and clean up a website template file. Here’s a breakdown of each part of the command:

1. **`sudo curl -o /var/www/html/2098_health.zip https://www.tooplate.com/zip-templates/2098_health.zip`**: 
   - `sudo`: Runs the command with superuser (root) privileges.
   - `curl -o /var/www/html/2098_health.zip`: Downloads the file from the specified URL (`https://www.tooplate.com/zip-templates/2098_health.zip`) and saves it as `2098_health.zip` in the `/var/www/html` directory.

2. **`&&`**: Logical AND operator, which ensures that the next command runs only if the previous command succeeds.

3. **`sudo unzip -d /var/www/html/ /var/www/html/2126_antique_cafe.zip`**:
   - `sudo`: Runs the command with superuser (root) privileges.
   - `unzip -d /var/www/html/`: Extracts the contents of the zip file into the `/var/www/html/` directory.
   - `/var/www/html/2126_antique_cafe.zip`: Specifies the path to the zip file to be unzipped.

4. **`&&`**: Logical AND operator, which ensures that the next command runs only if the previous command succeeds.

5. **`sudo rm -f /var/www/html/2126_antique_cafe.zip`**:
   - `sudo`: Runs the command with superuser (root) privileges.
   - `rm -f`: Removes (deletes) the specified file forcefully (without prompting for confirmation).
   - `/var/www/html/2126_antique_cafe.zip`: Specifies the path to the zip file to be deleted.

In summary, this command downloads the website template file, extracts its contents to the web server directory, and then deletes the downloaded zip file to clean up the directory.

---

- Download the 2nd website template by running the following command:

```
sudo curl -o /var/www/html/2119_gymso_fitness.zip https://www.tooplate.com/zip-templates/22119_gymso_fitness.zip && sudo unzip -d /var/www/html/ /var/www/html/2119_gymso_fitness.zip && sudo rm -f /var/www/html/2119_gymso_fitness.zip
```

- To set up your website's configuration, start by creating a new file in the Nginx sites-available directory. Use the following command to open a blank file in a text editor: **`sudo nano /etc/nginx/sites-available/cleaning

![4](img/4.png)

- Copy and paste the following code into the open text editor.

```
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/html/example.com;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- Edit the `root` directive within your server block to point to the directory where your downloaded website content is stored.

### Create An A Record

To make your website accessible via your domain name rather than the IP address, you'll need to set up a DNS record. I did this by buying my domain from Namecheap and then moving hosting to AWS Route 53, where I set up an A record.

> [!NOTE]
Visit [**Project1**](https://github.com/StrangeJay/DevOps_Projects/blob/f02b9151dd581eef3cec53c31e61066962e3641e/DevOpsCube/project1/project1.md) for instructions on how to create a hosted zone.

- In route 53, select the domain name and click on **Create record**.
