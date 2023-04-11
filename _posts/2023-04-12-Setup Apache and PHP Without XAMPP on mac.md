Tested on Mac Ventura 13.2.1 (22D68)

1. Install [httpd/apache](https://formulae.brew.sh/formula/httpd)
2. Install [php](https://formulae.brew.sh/formula/php#default)
3. Open `/usr/local/etc/httpd/httpd.conf` 
4. (Optional) If you want to have numerous hosts without a unique hostname each, uncomment `Include /usr/local/etc/httpd/extra/httpd-vhosts.conf` (remove #)
5. Uncomment `LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so`, handle url rewrite.
6. (Optional) Change default project directory in  
  DocumentRoot `"/Library/Projects/php"`   
  `<Directory "/Library/Projects/php">`
7. Create a separate apache conf file, let's say in `extras/` directory, with the name `php.conf`
8. Add a script to load php module in it.
  `#or /usr/local/opt/php/lib/httpd/modules/libphp.so`
  `LoadModule php_module /usr/local/opt/php/lib/httpd/modules/libphp.so`
9. Add these php configurations in the next line.
  ```
   <IfModule php_module>
    <FilesMatch \.php$>
      SetHandler application/x-httpd-php
    </FilesMatch>

    <IfModule dir_module>
     DirectoryIndex index.html index.php
    </IfModule>
  </IfModule>
  ```
10. start/restart httpd.
  `sudo brew services start httpd`
11. Run php. `sudo php -S 127.0.0.1:8080`. 
12. You can configure custom domain name in `etc/hosts` file.

References:
[Apache on macos](https://www.git-tower.com/blog/apache-on-macos/)


Possible problems:  
[Could not determine the server. ](https://stackoverflow.com/questions/18290683/httpd-could-not-reliably-determine-the-servers-fully-qualified-domain-name)   
Or you have an existing apache installed/configured already.


