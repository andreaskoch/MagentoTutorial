# Apache - Tips and Tricks

Things to know about Apache.


## Enable basic authentication for a website using the apache's .htaccess file

Enable basic authentication in the .htaccess file:

	AuthType basic
	AuthName "Some Name"
	AuthUserFile /var/www/.htpasswd
	Require valid-user

![](files/Authentication/Screenshot-htaccess-enable-Basic-Authentication.png)

Create a password file:

<!-- language: lang-sh -->

	# Create a file to store the users and their passwords
	touch /var/www/.htpasswd

	# Add a user named "user1" to the htpasswd file
	htpasswd /var/www/.htpasswd user1

![](files/Authentication/Screenshot-create-a-htpasswd-file.png)

Links:

- [apache.org: htpasswd - Manage user files for basic authentication](http://httpd.apache.org/docs/2.2/programs/htpasswd.html)

---

language: en
date: 2013-01-08
tags: Apache