### Samba_cheatsheet


###Samba###
| Action                                 | Command                                    |
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
|Test config| `testparm`|
|Change file/dir permissions - user - group - others - r= 4 w = 2 x = 1| `chmod 740 filename`|
|Change owner of file|`chown username groupname filename`|

###Samba share configuration parameters(ACL)###

| Explanation                                | Parameter                                  |
| :---                                    | :---                                       |
|[sharename]||
|    Comment   |`comment = string of anything really`|
|   Location of share     |`path = /srv/share/sharename`|
|      |`read only = yes`|
|  Guest can access     |`guest ok = yes`|
|   All clients connect as guest    |`guest only = yes`|
|  User write permissions    |`write-list=@group`|
|  Valid users for the share    |`valid users = @group`|
| Invalid users - deny access | `invalid users =  mark betty`| 
| User read permissions    |`read-list = @group`|
| Disallow anyone to read share  |`browseable = no`|
| Allows writing| `writeable=yes`|
|Maximum permissions for a new file (deny world)|`create mode = 0660`|
|Maximum permission for directory (deny world)|`directory mode = 0770`|
| Maximum conntections to a share at any given time| `max connections = 10 `| 

###Samba- Selinux booleans###
| Explanation                                | Boolean                                  |
| :---                                    | :---                                       |
|setsebool boolean [0,1]||
|Export nts/fusefs volumes|`samba_share_fusefs`|
|File/dir read only|`samba_export_all_ro`|
|File/dir read/write|`samba_export_all_rw`|
|Create home dirs| `samba_create_home_dirs`| 
|Share user home dirs| `samba_enable_home_dirs`| 
|Support home dirs| `samba_use_home_dirs`|
|Run unconfined scripts| `samba_run_unconfined`|
|Run as domain controller| `samba_domain_controller`|
|Run as portmapper| `samba_portmapper`|
|Allow modify public files - `labeled public_content_rw_t`|  `allow_smbd_anon_write`|






|Sources|Url|
|:---|:---|
|Users and security - In depth|`https://www.samba.org/samba/docs/using_samba/ch09.html`|
|Create users| `http://blog.sven.co.za/2010/06/02/samba-cheat-sheet-ubuntu/`|
|Basic info| `http://blog.sven.co.za/2010/06/02/samba-cheat-sheet-ubuntu/`|
|Ports, protocols and daemons - outdated iptables - use firewalld| `http://troy.jdmz.net/samba/fw/`|

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

| Action                                  | Command                                    |
| :---                                    | :---                                       |
| Is installed| `check-selinux-installation`| 
| Status            | `sestatus` |
| Enable selinux/get selinux|`setenforce 1` `getenforce`|
| Change context | `chcon` |
|Restore default SELinux settings|`restorecon /etc/hosts `|
|Restore label| `restorecon -R /srv/web`| 
| List allowed ports|`semanage port -l `| 
|List all security policy modules| `semodule -l `|
| Fix incorrect labels| `fixfiles relabel`| 
| Config files SELinux | `/etc/selinux/config `  |
| Booleans get  | `getsebool | grep X`) |
| Booleans set| `setsebool [0|1]`  |
| Graphic tool| `sudo system-config-selinux` |
|Add new user| `semanage login -a -s group user` `chcon -R -u group -r group /home/user`|
|Troubleshoot|`setroubleshoot` |
|Troubleshoot daemon| `setroubleshootd`|


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
