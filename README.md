# Nginx_Config_PHP_Framework
Config files for Nginx Server on Ubuntu 18.04 to serve CodeIgniter, Custom PHP Frameworks, Laravel, and other LEMP stack frameworks.

Note: This is an ongoing project for me as I learn how to use Nginx in place of Apache, this repository is intended to help beginner to intermediate PHP developers up and running for educational videos. I will work on security and better ways to improve the speed and performance of the setup as I learn more.

## Pre-requisites For Using This Source Code To Setup Nginx Server on Ubuntu 18.04

* Must be using PHP-FPM 5.0 or newer, however this code is set up for using PHP-FPM 7.2 with Ubuntu 18.04. Please make the necessary changes to the code to whatever version of PHP-FPM version you are using.

* Already have Nginx, PHP, and MySQL installed on your Ubuntu 18.04 server. The code should work with Ubuntu 16.04 or newer, however our code was built for 18.04. If you do not have the LEMP stack or Nginx setup on your machine, then please check out this great guide from Digital Ocean on how to setup the LEMP stack on Ubuntu at: https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-ubuntu-18-04 
You may download Nginx at: https://nginx.org/en/linux_packages.html#stable

* Have Nginx downnloaded and enabled, if you do not, below is the command line order to enable nginx as your localhost service.


> sudo systemctrl stop apache2.service

> sudo systemctrl enable nginx.service

> sudo systemctrol start nginx. service

* You have at minimum a index.php file for testing to see if nginx server is working properly.

* Have fireware software permissions set to allow access to the service.

* Have PHP-FPM installed and properly running.

## Instructions for Using Setting Up Nginx to Serve Index.php files on Ubuntu 18.04

1. Copy the files from /etc/sites-available/default to a new folder named /etc/sites-available/your_site.com, substituting your domain for your_site.com.

> sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/your_site.com

2. Edit the newly created file with the code in the repository labeled nginx_sitesavailable_yoursite.com using the nano text editor in the command line.

> sudo nano /etc/nginx/sites-available/your_site.com

3. Make sure the default server is in the /etc/nginx/sites-enabled/ directory.

> grep -R default_server /etc/nginx/sites-enabled/

4. Create a symbolic link the new directory to the sites-enabled directory. 

> sudo ln -s /etc/nginx/sites-available/your_site.com /etc/nginx/sites-enabled/

5. The /etc/nginx/conf.d/default.conf file is used to configure the default virtual host. Copy the  default.conf to create a new file names yoursite.com.conf. 

> sudo cp /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/yoursite.com.conf

6. Edit the nginx.conf file. Copy and paste the code in the repository into the newly created .conf file, changing yoursite.com to your own custom URL. 

> sudo nano /etc/nginx/nginx.conf.d/yoursite.com.conf

7. Restart the Nginx service

> sudo systemctl restart nginx.service

8. Test the configuration file using this command. You should get a response stating that sytax is ok and configuration was successful 

> sudo nginx -t

9. Edit the nginx hosts file using the Nano text editor. Add your domain to the list under localhost. If you are unsure how to do this, please cut and paste the code in the repository with the file name nginx_hosts.

> sudo nano /etc/hosts

8. It's a good idea to make sure file permissions are set to be able to write to your files, if you haven't already done so, the following commands will make sure all permissions are set for writing. Adjust setting based to your security needs.

> sudo chmod 757 /var/www

> sudo chmod 757 /var/www/your_site.com

> sudo chmod 757 /var/www/your_site.com/html

9. Restart the nginx service

>  sudo systemctl restart nginx.service

Your project should now be viewable at http://localhost/your_site.com/index.php 

If you do not see your application please check to make sure you have a index.php file first, then check the status of your nginx service. Also check to be sure you replaced all locations with your_site to your domain or project name.

## Troubleshooting Links and Other Helpful Nginx and LEMP Stack Resources

* Nginx Download - https://nginx.org/en/linux_packages.html#stable
* Official Nginx website: https://nginx.com

* Nginx Documentation - Official Nginx documentation link: https://docs.nginx.com/?_ga=2.71462611.194525721.1536891075-1736526540.1536770284

* 404 error help topic on Digital Ocean - https://www.digitalocean.com/community/questions/nginx-and-php-getting-error-404-with-scripts

* Nginx.Io - Website to help with config files for Nginx - https://nginxconfig.io

* Setup for PHP-FPM via Linode -  https://linode.com/docs/web-servers/nginx/serve-php-php-fpm-and-nginx/

* www-data and file permissions help link on StackExchange - https://superuser.com/questions/646062/granting-write-permissions-to-www-data-group

Spent a little time trying to figure this out so I thought I would share it. It is mainly for my re-use efforts, however feel free to make changes or make it better as needed. Hope it helps someone else out. Most of the tutorials on development are for the LAMP stack or use XAMPP or WAMPP, so I wanted to create some files for Nginx as I think it is a far better performing server then Apache.