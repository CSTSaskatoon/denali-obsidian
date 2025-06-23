```conf
# /etc/apache2/sites-available/fuckface.conf
<VirtualHost *:80>
	# Common practice to use *:80 if you are using name hosts (SeverName) because otherwise
	# the IP will override other hostnames
	ServerName www.fuckface.com

	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/fuckface.com/html
	
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/fuckface_access.log combined

	<Directory /var/www/fuckface.com/html>
		Require ip 10.36.106
	</Directory>

</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```