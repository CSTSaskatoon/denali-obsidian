## Q1
```bash
sudo adduser marcopolo # missing stuff
sudo adduser columbus # missing more stuff
su marcopolo
vi public_html/journeys.html
chmod 755 marcopolo

# Add the following to userdir.conf
Userdir disabled # student will be disabled with this, makes it a whitelist instead of blacklist
Userdir enabled columbus marcopolo
<Directory /explorers/*/public_html>
	Require all granted
	Options -Indexes # No indexes
</Directory>
```

### `journeys.html`
```html
<h1>In journeys.html</h1>
```

## Q2
1. Pair or triple up
2. Create a directory called `yourfirstname` under `/var/www/html`
3. Place an `index.html` there
4. Configure the directory so only other students can access it

```bash
sudo mkdir /var/www/html/denali
sudo echo "<h1>Welcome to Denali's fucking page</h1>" > /var/www/html/denali/index.html
sudo vi /etc/apache2/apache2.conf
# Add a directory like <Directory /var/www/html/denali></Directory>
# Require ip brody karbn
```