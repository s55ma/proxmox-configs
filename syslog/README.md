To forward Proxmox firewall rules to remote syslog, create file `/etc/rsyslog.d/50-default.conf` and paste this content:

```$ModLoad imfile
$InputFileName /var/log/pve-firewall.log
$InputFileTag pvefw
$InputFileStateFile stat-pvefw
$InputFileSeverity info
$InputFileFacility local3
$InputRunFileMonitor
local3.* @172.16.20.10:1518
```
Make sure to change `@172.16.20.10:1518` with your own remote syslog. @ is used for UDP. If you want to use TCP, use @@. Example: `local3.* @@172.16.20.10:1518`

Save file and restart rsyslog:

`systemctl restart rsyslog`
