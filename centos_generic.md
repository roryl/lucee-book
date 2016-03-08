# CentOS (Generic)

The following commands will setup a basic Lucee installation on a CentOS 6 server with Lucee, Apache and MySQL

Install Apache
> sudo yum -y install httpd

Install MySQL
>yum -y install mysql-server

Install the latest version of Lucee, grab the latest linux installer from [Lucee Downloads](http://lucee.org/downloads.html)

>wget http://d8yjolse1mixx.cloudfront.net/downloader.cfm/id/143/file/lucee-4.5.2.018-pl0-linux-x64-installer.run

Give permissions to execute the installer
>chmod 755 lucee-4.5.2.018-pl0-linux-x64-installer.run

Execute the installer, it will ask you a series of prompts. Usually the defaults are sufficient.

>./lucee-4.5.2.018-pl0-linux-x64-installer.run 

If you are scripting your installation, there are additional settings that can be helpful


>./lucee-4.5.2.018-pl0-linux-x64-installer.run --mode unattended --railopass 123456

This command will install Lucee with all of the default configuration options, bypassing the prompts, and will set a password for the admin of 123456
