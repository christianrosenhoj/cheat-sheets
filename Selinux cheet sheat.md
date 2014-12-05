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
