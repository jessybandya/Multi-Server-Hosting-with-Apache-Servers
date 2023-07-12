# Hosting React.js App on Apache Server

This guide will walk you through the steps to host a React.js app on an Apache server using XAMPP.

## React-js

-Add "homepage": "link to your web"
<BrowserRouter basename="/your-folder-path">
  ...
</BrowserRouter>


## Steps

1. Configure Apache Server

   - Navigate to the `feng` folder under your `ip address` directory. This is where your React app's build files should be placed.
   - Create an `.htaccess` file in the `feng` folder.
   - Add the following content to the `.htaccess` file:

     ```
      Options -Indexes
      DirectoryIndex index.html

     <IfModule mod_rewrite.c>
      RewriteEngine On
     RewriteBase /

     # Redirect all requests to index.html
     RewriteCond %{REQUEST_FILENAME} !-f
     RewriteCond %{REQUEST_FILENAME} !-d
     RewriteRule ^(.*)$ /index.html [L]
      </IfModule>

     ```

   - Open the `httpd.conf` file located in the `xampp/apache/conf` directory.
   - Find the `<Directory>` section that corresponds to your `feng` folder.
   - Add the following line within the `<Directory>` block or at the bottom as as a new block:

     ```
     IncludeOptional conf/extra/*.conf
     IncludeOptional conf.d/*.conf
     ```

   - Open the `httpd-vhosts.conf` file located in the `xampp/apache/conf/extra` directory.
   - Add the following virtual host configuration at the end of the file:

     ```
     <VirtualHost *:80>
     ServerAdmin sysadmin@uonbi.ac.ke
     DocumentRoot "/var/www/html/feng"
     ServerName unsa-feng.uonbi.ac.ke
     RewriteEngine On
     RewriteCond %{HTTPS} off
     RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
     ErrorLog "logs/unsa-feng.uonbi.ac.ke-error_log"
     CustomLog "logs/unsa-feng.uonbi.ac.ke-access_log" common
     </VirtualHost>


     <VirtualHost *:443>
     ServerAdmin sysadmin@uonbi.ac.ke
     DocumentRoot "/var/www/html/feng"
     ServerName unsa-feng.uonbi.ac.ke
     ServerAlias unsa-feng.uonbi.ac.ke
     SSLEngine on
     SSLCertificateFile /etc/pki/tls/certs/uonbi_ac_ke.crt
     SSLCertificateKeyFile /etc/pki/tls/certs/uonbi.ac.ke.key
     SSLCACertificateFile /etc/pki/tls/certs/comodo_cabundle.crt
     ErrorLog "logs/unsa-feng.uonbi.ac.ke-err.uonbi.ac.ke-access_log"
     CustomLog "logs/unsa-feng.uonbi.ac.ke-access_log" common
     </VirtualHost>
     ```

2. Restart Server


3. Access Your React App

   - Open your web browser.
   - Visit `Link to your web` (replace with the `ServerName` specified in the virtual host configuration) in the address bar.

## Conclusion

You have successfully hosted your React.js app on an Apache server using apache multi-server. Now you can access your app by visiting the specified URL in your browser.




#Happy Coding :)
