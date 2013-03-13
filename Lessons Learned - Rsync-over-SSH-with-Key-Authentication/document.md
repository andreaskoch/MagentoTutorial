# Rsync over SSH with key authentication

Using rsync and ssh to synchronize folders over the network.

## Setup the SSH login with key authentication 

Create a new ssh key pair:

<!-- language: lang-sh -->

	ssh-keygen -t rsa -b 2048 -f andy-rsync-key

 Move the public(!) key to the remote server:

<!-- language: lang-sh -->

	scp andy-rsync-key.pub andy@magento-azure.cloudapp.net:/home/andy/

Append the public key to the "authorized_keys" on your remote server:

<!-- language: lang-sh -->

	ssh -l andy magento-azure.cloudapp.net
	cat andy-rsync-key.pub >> .ssh/authorized_keys

Test the connection:

<!-- language: lang-sh -->

	ssh -l andy -i ~/.ssh/andy-rsync-key magento-azure.cloudapp.net

You should not be prompted for a password.

## Setup the folder synchronization

Test the synchronization:

<!-- language: lang-sh -->

	rsync --progress -avz -e "ssh -i /home/dev/.ssh/andy-rsync-key" /home/dev/git-master/ andy@magento-azure.cloudapp.net:/home/andy/git-master/

Create a shell script for the synchronization

<!-- language: lang-sh -->

	vi ~/bin/sync-git-master.sh

> `#!/bin/bash`
rsync --progress -avz --delete -e "ssh -i /home/dev/.ssh/andy-rsync-key" /home/dev/git-master/ andy@magento-azure.cloudapp.net:/home/andy/git-master/

	chmod 700 ~/bin/sync-git-master.sh

Schedule the script execution (every 5 minutes):

<!-- language: lang-sh -->

	crontab -e

> `# m h  dom mon dow   command
*/5 * * * * /home/dev/bin/git-master-sync.sh

## Links
- [Ubuntu Community: rsync](https://help.ubuntu.com/community/rsync)
- [Using Rsync and SSH - Keys, Validation and Automation](http://troy.jdmz.net/rsync/index.html)
- [SSH login without password](http://www.linuxproblem.org/art_9.html)
- [The Geek Stuff: How to Run Cron Every 5 Minutes, Seconds, Hours, Days, Months](http://www.thegeekstuff.com/2011/07/cron-every-5-minutes/)

---

language: en
date: 2013-01-17
tags: Linux, Backup, SSH