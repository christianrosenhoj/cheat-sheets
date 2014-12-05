### Samba_cheatsheet


###Samba###
| Actie                                  | Command                                    |
| :---                                    | :---                                       |
|Locatie samba conf. |  `/etc/samba/smb.conf`|

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
