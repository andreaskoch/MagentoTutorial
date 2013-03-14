# Automatically assign group ownership to new files and folders using the sticky bit

A simple chmod flag to enable inheritance of group ownership setings for files and folders on linux systems.

Shell command:

<!-- language: lang-sh -->

	# Add a sticky flag to a directory
	chmod g+s /name/of/directory

Be sure not to apply this flag to files and don't use the recursive (-R) flag.

## Links related to the linux stick bit

- [link:Linux-Web-Server-Development-Environment-File-Permissions]
- [LinuxQuestions.org: dir and group ownership automatic set
](http://www.linuxquestions.org/questions/linux-newbie-8/dir-and-group-ownership-automatic-set-649039/)
- [ComputerNetworkingNotes.com: Linux chmod commands sticky bit example and implementations](http://computernetworkingnotes.com/managing-file-system-security/sticky-bit.html)
- [YoLinux.com: Managing Group Access](http://www.yolinux.com/TUTORIALS/LinuxTutorialManagingGroups.html)

---

language: en
date: 2013-01-08
tags: Linux, Tipps & Tricks, Filesystem Permissions