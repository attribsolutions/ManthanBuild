To configure Server for the first time OR If ManthanBuild folder is deleted.. 
After git pull.. Log folder inside ManthanBuild will not be created automatically..
For that, create Log folder manually

Goto the log folder 
root@cbmdms64:/home/admin1/ManthanBuild# cd log/

And Create error.log file
root@cbmdms64:/home/admin1/ManthanBuild/log# nano error.log

root@cbmdms64:/home/admin1/ManthanBuild/log# ls
error.log  requests.log

After that, navigate to build folder (which is application root folder)
root@cbmdms64:/home/admin1/ManthanBuild/log# cd ..
root@cbmdms64:/home/admin1/ManthanBuild# cd build/

And Create .htaccess with below details:
root@cbmdms64:/home/admin1/ManthanBuild/build# nano .htaccess

<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_FILENAME} !-l
  RewriteRule . /index.html [L]
</IfModule>

Turn rewrite engine on by following command:
root@cbmdms64:/home/admin1/ManthanBuild/build# sudo a2enmod rewrite
Module rewrite already enabled

RESTART APACHE SERVER
root@cbmdms64:/home/admin1/ManthanBuild/build# sudo systemctl restart apache2
