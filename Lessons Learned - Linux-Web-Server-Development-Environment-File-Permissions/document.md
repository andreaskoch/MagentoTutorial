# Webserver file permissions for development environments

Some commands to realign the file permissions for linux-based Magento development environments.

Steps for a Magento installation on Ubuntu Linux:
1. Creaate a runtime user group
2. Addd all developers and the apache user to this group
3. Make the apache user the owner of the website
4. Assign the group ownership of the website to the new runtime user group
5. Set appropiate permissions
6. Make sure the group ownership is inherited for newly created files and folders

Example code:

	# Create a runtime user group
	sudo addgroup "magento-runtime"
	
	# Assign user to the new runtime user group
	sudo adduser developer1 magento-runtime
	sudo adduser www-data magento-runtime

	# Assign the ownership of all files and directories to the apache user "www-data"
	sudo chown www-data -R /var/www/vhosts/magento-admin-dev.example.com

	# Assign the group ownership to the "magento-runtime" group
	sudo chgrp magento-runtime -R /var/www/vhosts/magento-admin-dev.example.com

	# Assign permissions on all directories (Owner: full access, Group: full access, Others: read and execute)
	sudo find /var/www/vhosts/magento-admin-dev.example.com -type d -exec chmod 775 {} \;

	# Assign permissions on all files (Owner: read and write, Group: read and write, Others: read)
	sudo find /var/www/vhosts/magento-admin-dev.example -type f -exec chmod 664 {} \;

	# Set the stick-bit to inherit the group ownership to new files and folders
	sudo chmod g+s /var/www/vhosts/example


Moving the sample code into a shell script [file-link:set-webserver-group-permissions.sh.txt]:

[file-preview:set-webserver-group-permissions.sh.txt]


## Links
- [link:Linux-Automatic-Group-Ownership-with-the-Sticky-Bit]
- [chmod Tutorial](http://www.analysisandsolutions.com/code/chmod.htm)
- [tuxfiles:  How to change a file's owner and group in Linux](http://www.tuxfiles.org/linuxhelp/fileowner.html)
- [YoLinux.com: Managing Group Access](http://www.yolinux.com/TUTORIALS/LinuxTutorialManagingGroups.html)
- [Magento: Magento Filesystem Permissions](http://www.magentocommerce.com/wiki/1_-_installation_and_configuration/magento_filesystem_permissions)
- [LinuxQuestions.org: dir and group ownership automatic set](http://www.linuxquestions.org/questions/linux-newbie-8/dir-and-group-ownership-automatic-set-649039/)

---

language: en
date: 2013-01-08
tags: Linux, Tipps & Tricks, Filesystem Permissions, Magento, Development