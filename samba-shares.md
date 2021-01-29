---
description: How to setup samba shares for Mainsail
---

# Samba shares

### Samba shares

`sudo apt-get update`  
`sudo apt-get install samba samba-common-bin`

> _passwort setzen - wird der schritt benötigt?_  
> `sudo smbpasswd -a pi`

`sudo chmod -R 777 /home/pi/klipper_config`  
`sudo chmod -R 777 /home/pi/sdcard`

`sudo nano /etc/samba/smb.conf`

```text
[klipper_config]
comment = klipper config
path = /home/pi/klipper_config
writeable = Yes
only guest = Yes
create mask = 0777
directory mask = 0777
browseable = Yes
public = yes

[virtual_sdcard]
comment = virtual sdcard
path = /home/pi/sdcard
writeable = yes
only guest = yes
create mask = 0777
directory mask = 0777
browseable = yes
public = yes
```

`sudo service smbd restart`

