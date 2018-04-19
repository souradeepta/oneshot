# Sysadmin Knowledge

## Prep
[ ] Learn how to create unix accounts (users/groups) and how to secure processes, services, and filesystem access using them
[ ] Learn how to write good bash scripts - scripts that properly handle error conditions, for example
[ ] Learn how to automate deployments of application and/or database updates
[ ] Learn how to monitor the health of your web server, app server, and database servers.
[ ] Learn how to operate your VM provider's tools, especially how to automate basic operations like spinning up new instances.
[ ] Learn how to monitor performance
[ ] Learn what ulimit is, and how to adjust it
[ ] Learn to monitor overall system performance
[ ] Learn where all the logs for your applications are located
[ ] Learn how to set up environment variables for your applications
[ ] Learn key management
[ ] Learn basic networking, and the tools available for troubleshooting (ping, traceroute, nslookup, etc)
[ ] Learn how to install/remove/update packages. Then learn how to install versions of that software that are not part of the OS's package manager.
[ ] Learn basic file management (symlinking, permissions, etc)
[ ] Learn to use the source control and build systems that your development teams are using.
[ ] Learn enough about the programming languages that your devs are using that you can properly configure the runtime environment, and so you don't sound like a complete idiot when you ask them something about how their application works.
[ ] Learn to stop calling yourself "a devops".
[ ] Learn about the delivery methodology of the development team (Scrum, XP, Kanban, Waterfall [probably not!], etc)
[ ] Learn vim. That is, learn to use it without any plugins. (not getting into a religious debate here, it's just that vim is installed by default on just about every Linux distro; whereas emacs needs to be installed independently, and almost nobody does that).
[ ] Learn your company's configuration management system (assuming they have one - Puppet, Chef, Ansible, etc)
[ ] Learn how to install, configure, and operate the web server, app server, database server (if you don't have a separate team for that) and application(s) for the systems you will support.
[ ] Learn to troubleshoot and isolate problems. Don't be the guy who blames a problem on the application/developers, when the problem is really an OS/server/network configuration problem.
[ ] Learn how to mount network shares

## The real part

This is what I tell people to do, who ask me "how do I learn to be a Linux sysadmin?".

1) Set up a KVM hypervisor.
2) Inside of that KVM hypervisor, install a Spacewalk server. Use CentOS 6 as the distro for all work below. (For bonus points, set up errata importation on the CentOS channels, so you can properly see security update advisory information.)
3) Create a VM to provide named and dhcpd service to your entire environment. Set up the dhcp daemon to use the Spacewalk server as the pxeboot machine (thus allowing you to use Cobbler to do unattended OS installs). Make sure that every forward zone you create has a reverse zone associated with it. Use something like "internal.virtnet" (but not ".local") as your internal DNS zone.
4) Use that Spacewalk server to automatically (without touching it) install a new pair of OS instances, with which you will then create a Master/Master pair of LDAP servers. Make sure they register with the Spacewalk server. Do not allow anonymous bind, do not use unencrypted LDAP.
5) Reconfigure all 3 servers to use LDAP authentication.
6) Create two new VMs, again unattendedly, which will then be Postgresql VMs. Use pgpool-II to set up master/master replication between them. Export the database from your Spacewalk server and import it into the new pgsql cluster. Reconfigure your Spacewalk instance to run off of that server.
7) Set up a Puppet Master. Plug it into the Spacewalk server for identifying the inventory it will need to work with. (Cheat and use ansible for deployment purposes, again plugging into the Spacewalk server.)
8) Deploy another VM. Install iscsitgt and nfs-kernel-server on it. Export a LUN and an NFS share.
9) Deploy another VM. Install bakula on it, using the postgresql cluster to store its database. Register each machine on it, storing to flatfile. Store the bakula VM's image on the iscsi LUN, and every other machine on the NFS share.
10) Deploy two more VMs. These will have httpd (Apache2) on them. Leave essentially default for now.
11) Deploy two more VMs. These will have tomcat on them. Use JBoss Cache to replicate the session caches between them. Use the httpd servers as the frontends for this. The application you will run is JBoss Wiki.
12) You guessed right, deploy another VM. This will do iptables-based NAT/round-robin loadbalancing between the two httpd servers.
13) Deploy another VM. On this VM, install postfix. Set it up to use a gmail account to allow you to have it send emails, and receive messages only from your internal network.
14) Deploy another VM. On this VM, set up a Nagios server. Have it use snmp to monitor the communication state of every relevant service involved above. This means doing a "is the right port open" check, and a "I got the right kind of response" check and "We still have filesystem space free" check.
15) Deploy another VM. On this VM, set up a syslog daemon to listen to every other server's input. Reconfigure each other server to send their logging output to various files on the syslog server. (For extra credit, set up logstash or kibana or greylog to parse those logs.)
16) Document every last step you did in getting to this point in your brand new Wiki.
17) Now go back and create Puppet Manifests to ensure that every last one of these machines is authenticating to the LDAP servers, registered to the Spacewalk server, and backed up by the bakula server.
18) Now go back, reference your documents, and set up a Puppet Razor profile that hooks into each of these things to allow you to recreate, from scratch, each individual server.
19) Destroy every secondary machine you've created and use the above profile to recreate them, joining them to the clusters as needed.
20) Bonus exercise: create three more VMs. A CentOS 5, 6, and 7 machine. On each of these machines, set them up to allow you to create custom RPMs and import them into the Spacewalk server instance. Ensure your Puppet configurations work for all three and produce like-for-like behaviors.