# Nginx_Config_PHP_Framework
Config files for Nginx Server on Ubuntu 18.04 to serve CodeIgniter, Custom PHP Frameworks, Laravel, and other LEMP stack frameworks.

## Pre-requisites For Using Code To Setup Nginx Server on Ubuntu 18.04

* Must be using PHP-FPM 5.0 or newer, however this code is set up for using PHP-FPM 7.2. Please make the necessary changes to the code to whatever version of PHP-FPM you are using.

* You have already downloaded a framework like Laravel, Symfony, CodeIgnitor, or have your file folder structure set up to a similar MVC structure for use with a custom PHP framework and a index.php file in the public folder of the application.

* Already have Nginx installed on your Ubuntu 18.04 server. The code should work with Ubuntu 16.04 or newer. If you do not have the LEMP stack or Nginx setup on your machine, then please check out this great guide from Digital Ocean on how to setup the LEMP stack on Ubuntu at: https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-ubuntu-18-04

* Have Nginx enabled

> sudo systemctrl stop apache2.service

> sudo systemctrl enable nginx.service

> sudo systemctrol start nginx. service

## Instructions for Using Setting Up Nginx to Serve Index.php files on Ubuntu 18.04

1. Copy the files from /etc/sites-available/default to a new folder named /etc/sites-available/your_site.com, substituting your domain for your_site.com.

> sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/your_site.com

2. Edit the newly created file with the code in the repository labeled nginx_sitesavailable_yoursite.com using the nano text editor in the command line.

> sudo nano /etc/nginx/sites-available/your_site.com

3. Make sure the default server is in the /etc/nginx/sites-enabled/ directory.

> grep -R default_server /etc/nginx/sites-enabled/

4. Link the new directory to the sites-enabled directory. 

> sudo ln -s /etc/nginx/sites-available/your_site.com /etc/nginx/sites-enabled/

5. Edit the nginx.conf file. Copy and paste the code in the repository if the default nginx setting doesn't work for you. This step may be optional for some users.

> sudo nano /etc/nginx/nginx.conf

6. Create .htaccess file in the public folder of your project or framework. Some frameworks have .htaccess files built in, try the default settings before adding a new .htaccess file to your project. Below is the .htaccess that works with this code:

<IfModule mod_rewrite.c>
  Options -Multiviews
  RewriteEngine On
  RewriteBase /grandstrandmvc.com/public
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteRule  ^(.+)$ index.php?url=$1 [QSA,L]
</IfModule>

7. Test the configuration file using this command. You should get a response stating that sytax is ok and configuration was successful 

> sudo nginx -t

8. Edit the nginx hosts file using the Nano text editor. Add your domain to the list under localhost. If you are unsure how to do this, please cut and paste the code in the repository with the file name nginx_hosts.

> sudo nano /etc/hosts

9. Change WWW Data Ownership, Set Users, and Set File Permissions

> sudo chmod 775 /var/www

> sudo chmod 775 /var/www/grandstrandmvc.com

> sudo chmod 775 /var/www/grandstrandmvc.com/html

> sudo chown -R www-data:www-data /var/www/grandstrandmvc.com

> sudo chown -R www-data:www-data /var/www/grandstrandmvc.com/html

> sudo chown -R $USER:$USER /var/www/grandstrandmvc.com

10. Restart the nginx service

>  sudo systemctl restart nginx.service

Your project should now be viewable at http://localhost/your_site.com/public/index.php If you do not see your application please check to make sure you have a index.php file first, then check the status of your nginx service. Also check to be sure you replaced all locations with your_site to your domain or project name.

## Troubleshooting Links and Other Helpful Nginx and LEMP Stack Resources

* Nginx Download - Official Nginx website: https://nginx.com

* Nginx Documentation - Official Nginx documentation link: https://docs.nginx.com/?_ga=2.71462611.194525721.1536891075-1736526540.1536770284

* 404 error help topic on Digital Ocean - https://www.digitalocean.com/community/questions/nginx-and-php-getting-error-404-with-scripts

* Nginx.Io - Website to help with config files for Nginx - https://nginxconfig.io

* Setup for PHP-FPM via Linode -  https://linode.com/docs/web-servers/nginx/serve-php-php-fpm-and-nginx/

Spent a little time trying to figure this out so I thought I would share it. It is mainly for my re-use efforts, however feel free to make changes or make it better as needed. Hope it helps someone else out. Most of the tutorials on development are for the LAMP stack or use XAMPP or WAMPP, so I wanted to create some files for Nginx as I think it is a far better performing server then Apache.
