## Checklist

| Check		| Task
| :--		| :--
|			| Hardware (are cables connected?).
|			| IP (does the VM network card have the correct IP config).
|			| Services (nmbd, smbd) are enabled.
|			| Users - created and configured
|			| Samba conf (smb.conf) configured
|			| SELinux configured (getsebool: samba_enable_home_dirs, samba_export_all_rw)
|     | Other security settings are enabled and configured (firewalld)