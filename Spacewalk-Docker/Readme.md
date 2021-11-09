## Inside Spacewalk-external-psql Folder
```
- First build Dockrfile.pg and run it... We need 172.17.0.2
- DB: postgres
- Password: aditya
- User: postgres
Inside Postgres Container  CREATE EXTENSION pltclu;
```
```
aditya@aditya:~/Desktop/Spacewalk/Mark3$ cat jpackage-generic.repo 
[jpackage-generic]
name=JPackage generic
baseurl=http://mirrors.dotsrc.org/pub/jpackage/5.0/generic/free/
mirrorlist=http://www.jpackage.org/mirrorlist.php?dist=generic&type=free&release=5.0
failovermethod=priority
enabled=1
gpgcheck=1
gpgkey=http://www.jpackage.org/jpackage.asc

```
```
Here are some points regarding spacewalk

1) We cannot use Azure postgres managed service because for creating the schema in database
spacwalk user need to have superuser permission, As Azure postgres managed service is a 
PAAS solution only microsoft can be the superuser also mentioned in official docs 

2) Spacewalk provides the spacewalk-setup-postgresql package by which It creates DB schema in same 
machine we have to use that, so for spacewalk their will be only one docker image with 
spacewalk and postgresql database combined

3) We can also setup spacewalk with external postgres container so two containers
one for spacewalk and one for postgres

4)We have to expose these ports for spacewalk : 80, 443, 5222, 68, 69

5)we have to run Spacewalk container in privileged mode then only it will works fine

6)Spacewalk creates the default self signed certificate but when we open it to browser 
  it give security issue because by default it redirect http to https
```
---------------

#### Error Reference Links 
```
https://marc.info/?l=spacewalk-list&m=153792669712420&w=2

https://bugzilla.redhat.com/show_bug.cgi?id=1506597

https://listman.redhat.com/archives/spacewalk-list/2019-January/msg00014.html


```
