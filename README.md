# Hardening-CIS
**Description**

Comply with CIS Standards for AIX servers.

**Overview**

CIS provides a prescriptive guidance for establishing a secure configuration posture for AIX servers.

Not all the checks to comply with CIS have been added but if you run this playbook, your server will be compliant at 99 %

**Requisites**

This has been tested for AIX 7.1 and AIX 7.2

**Explanation**

The playbook is formed of several tasks, roles and variables.
The variables are stored under 2 different files and trhey are used for fiferent tasks.
/etc/ansible/vars/hardening_vars.yml stores variables assigned to configure network parameters in these two tasks "Check tcp/ip parameters" (tcpip)
and "Check tcp/ip parameters - nfs" (nfso)

/etc/ansible/vars/usr_vars.yml stores variables assigned to configure users settings in this task "Check if admin accounts exist" (id)

There are 2 roles created:

 ***hk*** which is used for housekeeping
 
 ***gpm*** which is used to handle files which should keep some kind of special permissions.
	Sometimes for the correct functioning of applications and systems, some files need to keep some permissions
	(suid, sgid, worldwide writable) although they are not compliant with CIS standards.
	
  The role includes three tasks, one for each kind of special permissions. 
  The way it works is copying the template of allowed files
  into the target server, copying a script that translates the wildcards stated in the file into the real file if it exists on 
  the server and then and then comparing those files with the files that are found with that special bit.
  The files found in the system which are not allowed get their special bit removed.
	
E.g if /*/products/*/oracle is on the files allowed, the script will translate that file into /sgg/products/bin/oracle which is the file 
that exists on the server. That file won't get the special bit removed.
	
