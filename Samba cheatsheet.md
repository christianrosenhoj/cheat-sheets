### Samba_cheatsheet


###Samba###
| Actie                                  | Command                                    |
| :---                                    | :---                                       |
|Locatie samba conf.- see `Samba share configuration parameters` |  `/etc/samba/smb.conf`|
|SAMBA service| `smbd`| 
|SAMBA starts on boot| `/etc/init.d/smbd` `chkconfig smb on` |
|NetBios nameserver service | `nmbd.service`|
|NetBios poorten| `137``138``139`|
|Samba service RUNNING and LISTENING|`netstat -ntl | grep portnumber` |
|Add user| `smbpasswd -a username`|
|Enable user| `smbpasswd -e username`|
|Show users/groups| `getent passwd` `getent group`|

###Samba share configuration parameters###

| :---                                    | :---                                       |
|Locatie samba conf.- see `Samba share configuration parameters` |  `/etc/samba/smb.conf`|


|[sharename]|x|
|    x   |comment = string of anything really|
|   Location of share     |path = /srv/share/sharename|
|   x    |read only = yes|
|    x    |guest ok = yes|
|   x    | guest only = yes|
|  User write permissions    |write-list=@group|
|  Valid users for the share    |valid users = @group|
| User read permissions    |read-list|
| Disallow anyone to read share   |browseable = no|
| Allows writing| `writeable=yes`|

### Tools
* `yum install setroubleshoot`, gevolgd door: `service auditd restart`
* `yum install xorg-x11-xauth policycoreutils-gui bitmap-fixed-fonts`
* `yum install net-tools`
* `repoquery -qf */netstat */lsof */nmap`
      * Wanneer niet geïnstalleerd: `yum install yum-utils`
* IP-conflicten opsporen: `sudo yum install arp-scan`
<br> en 
    `arp-scan -I eth0 -l`
* _yum install nmap_


###SELinux ###

| Actie                                  | Command                                    |
| :---                                    | :---                                       |
| Status controleren                | `sestatus` |
| Herstellen initiële SELinux-settings| `restorecon -R -v [target-folder]`(bijv. /var/www) |
| In de logs controleren op output van setroubleshoot | `grep setroubleshoot /var/log/messages` |
| Config files SELinux | `/etc/selinux/config `                         |
| Labeling controleren (optie -Z) | `ls -lZ [/usr/sbin/httpd]`                       |
| Change context | `chcon` |
| Booleans opvragen | `getsebool | grep X`) |
| Booleans instellen| `setsebool [0|1]`  |
| (na install setroubleshoot) | `sudo sealert -l [de opgegeven code]` |
| Grafische tool| `sudo system-config-selinux` |


###Nuttige config files###
| Path							| Function
| :---							| :---
| `/etc/samba/smb.conf`			| Samba
| `/etc/vsftpd/vsftpd.conf`		| FTP

### Firewall ###
* Firewall: /etc/sysconfig/iptables
    * systemctl restart iptables.service
| Action							| Function
| :---                                    | :---                                       |
| Currently enabled features       | `firewall-cmd --list-all-zones`                                  |
| Enable a port in zone            | `firewall-cmd [--permanent] [--zone=ZONE] --add-port=80/tcp`     |


### Services controleren ###
Indien deze uitstaan, aanzetten.
* SAMBA: 
    * systemctl status smb.service (daemon)
    * systemctl status nmb.service (daemon)
