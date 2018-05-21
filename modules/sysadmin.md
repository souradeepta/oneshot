# Sysadmin Knowledge

## Prep
- [ ] Learn how to create unix accounts (users/groups) and how to secure processes, services, and filesystem access using them
- [ ] Learn how to write good bash scripts - scripts that properly handle error conditions, for example
- [ ] Learn how to automate deployments of application and/or database updates
- [ ] Learn how to monitor the health of your web server, app server, and database servers.
- [ ] Learn how to operate your VM provider's tools, especially how to automate basic operations like spinning up new instances.
- [ ] Learn how to monitor performance
- [ ] Learn what ulimit is, and how to adjust it
- [ ] Learn to monitor overall system performance
- [ ] Learn where all the logs for your applications are located
- [ ] Learn how to set up environment variables for your applications
- [ ] Learn key management
- [ ] Learn basic networking, and the tools available for troubleshooting (ping, traceroute, nslookup, etc)
- [ ] Learn how to install/remove/update packages. Then learn how to install versions of that software that are not part of the OS's package manager.
- [ ] Learn basic file management (symlinking, permissions, etc)
- [ ] Learn to use the source control and build systems that your development teams are using.
- [ ] Learn enough about the programming languages that your devs are using that you can properly configure the runtime environment, and so you don't sound like a complete idiot when you ask them something about how their application works.
- [ ] Learn to stop calling yourself "a devops".
- [ ] Learn about the delivery methodology of the development team (Scrum, XP, Kanban, Waterfall [probably not!], etc)
- [ ] Learn vim. That is, learn to use it without any plugins. (not getting into a religious debate here, it's just that vim is installed by default on just about every Linux distro; whereas emacs needs to be installed independently, and almost nobody does that).
- [ ] Learn your company's configuration management system (assuming they have one - Puppet, Chef, Ansible, etc)
- [ ] Learn how to install, configure, and operate the web server, app server, database server (if you don't have a separate team for that) and application(s) for the systems you will support.
- [ ] Learn to troubleshoot and isolate problems. Don't be the guy who blames a problem on the application/developers, when the problem is really an OS/server/network configuration problem.
- [ ] Learn how to mount network shares

## The real part

This is what I tell people to do, who ask me "how do I learn to be a Linux sysadmin?".

- [ ] Set up a KVM hypervisor.
- [ ] Inside of that KVM hypervisor, install a Spacewalk server. Use CentOS 6 as the distro for all work below. (For bonus points, set up errata importation on the CentOS channels, so you can properly see security update advisory information.)
- [ ] Create a VM to provide named and dhcpd service to your entire environment. Set up the dhcp daemon to use the Spacewalk server as the pxeboot machine (thus allowing you to use Cobbler to do unattended OS installs). Make sure that every forward zone you create has a reverse zone associated with it. Use something like "internal.virtnet" (but not ".local") as your internal DNS zone.
- [ ] Use that Spacewalk server to automatically (without touching it) install a new pair of OS instances, with which you will then create a Master/Master pair of LDAP servers. Make sure they register with the Spacewalk server. Do not allow anonymous bind, do not use unencrypted LDAP.
- [ ] Reconfigure all 3 servers to use LDAP authentication.
- [ ] Create two new VMs, again unattendedly, which will then be Postgresql VMs. Use pgpool-II to set up master/master replication between them. Export the database from your Spacewalk server and import it into the new pgsql cluster. Reconfigure your Spacewalk instance to run off of that server.
- [ ] Set up a Puppet Master. Plug it into the Spacewalk server for identifying the inventory it will need to work with. (Cheat and use ansible for deployment purposes, again plugging into the Spacewalk server.)
- [ ] Deploy another VM. Install iscsitgt and nfs-kernel-server on it. Export a LUN and an NFS share.
- [ ] Deploy another VM. Install bakula on it, using the postgresql cluster to store its database. Register each machine on it, storing to flatfile. Store the bakula VM's image on the iscsi LUN, and every other machine on the NFS share.
- [ ] Deploy two more VMs. These will have httpd (Apache2) on them. Leave essentially default for now.
- [ ] Deploy two more VMs. These will have tomcat on them. Use JBoss Cache to replicate the session caches between them. Use the httpd servers as the frontends for this. The application you will run is JBoss Wiki.
- [ ] You guessed right, deploy another VM. This will do iptables-based NAT/round-robin loadbalancing between the two httpd servers.
- [ ] Deploy another VM. On this VM, install postfix. Set it up to use a gmail account to allow you to have it send emails, and receive messages only from your internal network.
- [ ] Deploy another VM. On this VM, set up a Nagios server. Have it use snmp to monitor the communication state of every relevant service involved above. This means doing a "is the right port open" check, and a "I got the right kind of response" check and "We still have filesystem space free" check.
- [ ] Deploy another VM. On this VM, set up a syslog daemon to listen to every other server's input. Reconfigure each other server to send their logging output to various files on the syslog server. (For extra credit, set up logstash or kibana or greylog to parse those logs.)
- [ ] Document every last step you did in getting to this point in your brand new Wiki.
- [ ] Now go back and create Puppet Manifests to ensure that every last one of these machines is authenticating to the LDAP servers, registered to the Spacewalk server, and backed up by the bakula server.
- [ ] Now go back, reference your documents, and set up a Puppet Razor profile that hooks into each of these things to allow you to recreate, from scratch, each individual server.
- [ ] Destroy every secondary machine you've created and use the above profile to recreate them, joining them to the clusters as needed.
- [ ] Bonus exercise: create three more VMs. A CentOS 5, 6, and 7 machine. On each of these machines, set them up to allow you to create custom RPMs and import them into the Spacewalk server instance. Ensure your Puppet configurations work for all three and produce like-for-like behaviors.

## Syllabus

### Tools
- [ ] [cron help](https://healthchecks.io/docs/cron/)

### Resources
- [ ] [Meta Advice for sysadmin](https://sysadmincasts.com/episodes/25-bits-sysadmins-should-know)
- [ ] [SABook](http://sabok.org)
- [ ] [opsschool](http://www.opsschool.org/en/latest/introduction.html)
- [ ] [Sysadmin Evaluation Sheet](https://www.docs.google.com/spreadsheets/d/1FBr20VIOePQH2aAH2a_6irvdB1NOTHZaD8U5e2MOMiw/pub?output=html)
- [ ] [Awesome sysadmin](https://github.com/kahun/awesome-sysadmin)
- [ ] [Good Links](https://www.gerrywilliams.net/bookmarks/)

### Level 0
- Basic Stuff as a user I should know
    - learn curl
    - learn to use tor
    - read git pro
    - [VPN Setup by varun](https://varunpriolkar.com/2018/05/ultimate-openvpn-setup-to-rule-them-all/)
    - [Bash Scripting](https://github.com/anordal/shellharden/blob/master/how_to_do_things_safely_in_bash.md)
    - [App recomendations](https://lobste.rs/s/8xtyxo/f_droid_app_recommendation_thread)
    - [Docker](https://takacsmark.com/dockerfile-tutorial-by-example-dockerfile-best-practices-2018/)
    - [Core Linux Concepts](https://www.funtoo.org/Category:Linux_Core_Concepts)
    - [Moving in CLI](https://clementc.github.io/blog/2018/01/25/moving_cli/)
    - [Difference between Tmux and Screen](https://wtanaka.com/node/8136)
    - [How groups work in linux](https://jvns.ca/blog/2017/11/20/groups/)
    - [TCPdump Primer](https://danielmiessler.com/study/tcpdump/)
    - [HTOP explained - I](https://peteris.rocks/blog/htop/)
    - [HTOP explained - II](https://codeahoy.com/2017/01/20/hhtop-explained-visually/)
    - [HTOP explained - III](https://lobste.rs/s/eh5u4f/managing_processes_with_htop)
    - [Linux CPU stats](http://blog.scoutapp.com/articles/2015/02/24/understanding-linuxs-cpu-stats)
    - [EFI Boot Process I](http://jdebp.eu./FGA/efi-boot-process.html)
    - [EFI Boot Process II (More Practical)](https://www.rodsbooks.com/efi-bootloaders/index.html)
    - [UEFI Boot Process (Too much blah!)](https://www.happyassassin.net/2014/01/25/uefi-boot-how-does-that-actually-work-then/)
    - [Home Backup Strategy](https://www.zachary.com/posts/how-to-data/)
    - [Tor best practices](https://riseup.net/en/security/network-security/tor/onionservices-best-practices)

### Tutorials
- [ ] [pfsense playlist](https://www.youtube.com/playlist?list=PLE726R7YUJTePGvo0Zga2juUBxxFTH4Bk)
- [ ] [Command line text processing Book](https://github.com/learnbyexample/Command-line-text-processing)
- [ ] [Sysadmin casts](https://sysadmincasts.com)
- BCHS Webserver
    - [ ] [Tutorial](https://learnbchs.org/index.html)
    - [ ] [Discussion](https://lobste.rs/s/2c4hvd/bchs_bsd_c_httpd_sqlite)
- [ ] [Interactive Ansible Tutorial](https://github.com/turkenh/ansible-interactive-tutorial)
- [ ] [sudo syntax](http://toroid.org/sudoers-syntax)

- Understanding Virtulization
    - [ ] [Vagrant KnowHow](https://zwischenzugs.com/2017/10/27/ten-things-i-wish-id-known-before-using-vagrant/)

- Understanding Containers
    - [ ] [Intro](http://doger.io)
    - [ ] [AWS EC2 and Docker Subscribed Video Series](https://awsdevops.io/courses/190849/lectures/2902055)
    - [ ] [Building Containers](https://blog.kintoandar.com/2018/01/Building-healthier-containers.html)
    - [ ] [Why containers](http://www.tedinski.com/2018/04/03/why-containers.html)
    - [ ] [Container Internals P-I]( http://rabbitstack.github.io/operating%20systems/linux-containers-internals-part-i/)
    - [ ] Theres a bocker named repo in github, check it.
    - [ ] [Handcrafted Containers](http://blog.z3bra.org/2016/03/hand-crafted-containers.html)
    - [ ] [Linux Namespaces](https://medium.com/@teddyking/linux-namespaces-850489d3ccf)
    - [ ] [Linux Namespaces II](https://blogs.igalia.com/dpino/2016/04/10/network-namespaces/)
    - [ ] [Workshop on Linux Containers](https://github.com/Fewbytes/rubber-docker)
    - [ ] [Intro to LXD](https://blog.scottlowe.org/2015/05/06/quick-intro-lxd/)
    - [ ] [Docker VS Binaries](https://lobste.rs/s/zz9oc8/why_would_anyone_choose_docker_over_fat)
    - [ ] [LXC Networking](http://containerops.org/2013/11/19/lxc-networking/)

- War stories and Case Studies
    - [Monitoring at soundcloud](https://developers.soundcloud.com/blog/prometheus-monitoring-at-soundcloud)
    - [Learn redis the hard way trivago](http://tech.trivago.com/2017/01/25/learn-redis-the-hard-way-in-production/)
    - [Fastest Site in the world](https://hackernoon.com/10-things-i-learned-making-the-fastest-site-in-the-world-18a0e1cdf4a7)
    - [Crawling 40 Billion Pages](http://www.michaelnielsen.org/ddi/how-to-crawl-a-quarter-billion-webpages-in-40-hours/)
    - [Stop using gzip!](http://imoverclocked.blogspot.in/2015/12/for-love-of-bits-stop-using-gzip.html)
    - [Adventures in /usr/bin](https://ablagoev.github.io/linux/adventures/commands/2017/02/19/adventures-in-usr-bin.html)
    - [Why nix](https://yakking.branchable.com/posts/what-and-why-nix/)
    - [Memcached-Backed Content Infrastructure Khanacademy](http://engineering.khanacademy.org/posts/memcached-fms.htm)
    - [Dropbox Optimize for web](https://blogs.dropbox.com/tech/2017/09/optimizing-web-servers-for-high-throughput-and-low-latency/)
    - [Dumbsmash Scalling with 3 engg]( https://stackshare.io/dubsmash/dubsmash-scaling-to-200-million-users-with-3-engineers)
    - [Don't parse output of ls](http://mywiki.wooledge.org/ParsingLs)

- Sysadmin Tools
    - [Compare nuster and squid](https://github.com/jiangwenyuan/nuster/wiki/Web-cache-server-performance-benchmark:-nuster-vs-squid)

- SSL, SSH & Sysadmin & Home Security
    - [ ] First know the difference between SSH and SSL then OpenSSH and OpenSSL
    - [ ] [SSH for everything](https://lobste.rs/s/oufswu/why_aren_t_we_using_ssh_for_everything)
    - [ ] [Security basics with GPG, OpenSSH, OpenSSL and Keybase](https://www.integralist.co.uk/posts/security-basics/)
    - [ ] [Own identity using gpg](http://www.saminiir.com/establish-cryptographic-identity-using-gnupg/)
    - [ ] [Upgrading SSH Keys](https://blog.g3rt.nl/upgrade-your-ssh-keys.html)
    - [ ] [Using OpenSSL to create certificates]( https://www.blinkingcaret.com/2017/02/01/using-openssl-to-create-certificates/)
    - [ ] [SSH vs Open VPN](https://lobste.rs/s/5ewzcx/ssh_vs_openvpn_for_tunneling)
    - [ ] [SSH for fun](https://karla.io/2016/04/30/ssh-for-fun-and-profit.html)
    - [ ] [Zen of pgp](https://medium.com/@thegrugq/the-zen-of-pgp-6f55d44657dd)
    - [ ] [SSH for everything](https://medium.com/@shazow/ssh-how-does-it-even-9e43586e4ffc)
    - [ ] [SSH Tips](http://markmims.com/2015/06/01/ssh-tips.html)
    - [ ] [Alerting on SSH](https://jpmens.net/2018/03/25/alerting-on-ssh-logins/)
    - [ ] [How OpenPGP Works](https://www.foo.be/2016/12/OpenPGP-really-works)
    - [ ] [WTF is this](https://www.reddit.com/r/commandline/comments/8bfxq4/good_free_ssh_shell_accounts/)
    - [ ] [SSH Login](https://lobste.rs/s/vy9uj7/web_login_using_ssh)
    - [ ] [SSH Login II](https://archive.is/7qP7i)
    - [ ] [Learning GPG](https://russellparker.me/post/2018/04/10/how-learning-gpg-is-like-learning-git/)
    - [ ] [How to use PGP](https://ssd.eff.org/en/module/how-use-pgp-linux)
    - [ ] [Encypted email](https://lobste.rs/s/zbzm9m/encrypted_email_is_still_pain_2017)
    - [ ] [SSH keys(few wrong facts in numbers, beware)](https://kyleisom.net/articles/ssh_keys.html) 
    - [ ] [GPG docs](http://futureboy.us/pgp.html)
    - [ ] [SSH History](https://www.ssh.com/ssh/port)
    - [ ] [Advanced intro GPG](https://begriffs.com/posts/2016-11-05-advanced-intro-gnupg.html)

- Doing Practical things
    - [Running own DNS server](https://lobste.rs/s/mrgro8/how_why_i_run_my_own_dns_servers)
    - [Running own DNS server II](https://lobste.rs/s/en12xe/host_your_own_dns_over_https_server_for)
    - [SOCKS Proxy](https://ma.ttias.be/socks-proxy-linux-ssh-bypass-content-filters/)
    - [OpenBSD webserver](https://www.romanzolotarev.com/openbsd/webserver.html)
    - [Webapp with fastcgi and C](https://kristaps.bsd.lv/absdcon2016/)
    - [Own Mail Server](https://www.c0ffee.net/blog/mail-server-guide)
    - [OpenVPN guide](https://www.c0ffee.net/blog/openvpn-guide)
    - [IRC Jumper](https://wiki.znc.in/ZNC)

- Text Processing
    - [Skip Grep use awk](http://blog.jpalardy.com/posts/skip-grep-use-awk/)
    - [Sculpting Text](http://matt.might.net/articles/sculpting-text/)
    - [Text Processing VS Hadoop]( https://aadrake.com/command-line-tools-can-be-235x-faster-than-your-hadoop-cluster.html)

- Bash
    - [Bash Guide](http://mywiki.wooledge.org/BashGuide)
    - [Bash Scripting Mistakes](http://www.pixelbeat.org/programming/shell_script_mistakes.html)
    - [Robust Shell Scripts](https://www.davidpashley.com/articles/writing-robust-shell-scripts/)
    - [Bash by example](http://matt.might.net/articles/bash-by-example/)
    - [Mistakes in bash](https://blog.janestreet.com/when-bash-scripts-bite/)
    - [Style Guide](https://google.github.io/styleguide/shell.xml)
    - [Advanced Guide](http://www.tldp.org/LDP/abs/html/index.html)
    - [Bash One liners](http://www.catonmat.net/blog/bash-one-liners-explained-part-one/)

- Scaling  Intro
    - [Good Loadbalancing and Proxy Intro](https://blog.envoyproxy.io/introduction-to-modern-network-load-balancing-and-proxying-a57f6ff80236)
    - [Memcached V/S Redis](https://lobste.rs/s/elmdha/memcached_redis)
    - [Scaling with load balancing](https://blog.vivekpanyam.com/scaling-a-web-service-load-balancing/)
    - [HFT guy on loadbalancing]( https://thehftguy.com/2016/10/03/haproxy-vs-nginx-why-you-should-never-use-nginx-for-load-balancing/)

- Advanced Load Balancing
    - [ ] [Consistent Hashing in viemo]( https://medium.com/vimeo-engineering-blog/improving-load-balancing-with-a-new-consistent-hashing-algorithm-9f1bd75709ed)
    - [ ] [Consistent Hashing google]( https://research.googleblog.com/2017/04/consistent-hashing-with-bounded-loads.html)
