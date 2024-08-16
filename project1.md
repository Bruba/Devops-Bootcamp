# Setup a Static Website Using Nginx
 - these are the steps to accomplish this
### Create An Ubuntu Server on AWS
- create an account on AWS
- locate EC2
- EC2 enables you to start varoius operating systems within the AWS cloud environment

- Click on **Launch Instance**

![1](img/1.png)

- you can see a variety of instances, for this i chose Ubuntu
- **Name** your instance and select the **Ubuntu** AMI.

![2](img/2.png)

- confirm that the instance is up and running

![3](img/3.png)

### Create and Assign an Elastic IP

- Select **Elastic IPs** under **Network & Security**

### Install Nginx
- Execute the following commands.

`sudo apt update`

`sudo apt upgrade`

`sudo apt install nginx`

- Start your Nginx server by running the **`sudo systemctl start nginx`** command, enable it to start on boot by executing **`sudo systemctl enable nginx`**, and then confirm if it's running with the **`sudo systemctl status nginx`** command.

![5](img/5.png)

- Download your website template from your preferred website by navigating to the website, locating the template you want, and obtaining the download URL for the website.

### Create An A Record
To make your website accessible via your domain name rather than the IP address, you'll need to set up a DNS record. I did this by buying my domain from Porkbun and then moving hosting to AWS Route 53, where I set up an A record.

- Go back to your AWS console, search for **Route 53①**, and then choose **Route 53②** from the list of services shown.

- Select **Create hosted zones** and click on **Get started**.

- Enter your **Domain name**, choose **Public hosted zone** and then click on **Create hosted zone**.

- Select the **created hosted zone** and copy the assigned **Values**.

- Go back to your domain registrar and select **Custom DNS** within the **NAMESERVERS** section.

![9](img/9.png)

- Head back to your AWS console and click on **Create record**.

![6](img/6.png)

### Install certbot and Request For an SSL/TLS Certificate

- Install certbot by executing the following commands:
**`sudo apt update`**
**`sudo apt install certbot python3-certbot-nginx`**

- Execute the **`sudo certbot --nginx`** command to request your certificate. Follow the instructions provided by certbot and select the domain name for which you would like to activate HTTPS.

![7](img/7.png)

- Goto **`https://<domain name>`** to view your website.

![8](img/8.png)