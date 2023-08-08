# Run Control
Traditionally, the shell script /etc/rc.local used by developers and Linux sysadmin to call other scripts or commands after all services are loaded.

Edit `/etc/rc.local` file in your raspberry pi.
```
sudo vim /etc/rc.local
```
Make sure to set executable permission
```
sudo chmod +x /etc/rc.local
```
Edit `rc-local.service` in `/etc/systemd/system` directory.
```
sudo vim /etc/systemd/system
```
Add `rc-local.service` to system daemon
```
sudo systemctl enable rc-local.service
```
Reboot the system and check the status.
```
sudo systemctl status rc-local.service
```
If success, it would look something like this:
```
* rc-local.service - /etc/rc.local Compatibility
     Loaded: loaded (/etc/systemd/system/rc-local.service; enabled; vendor preset: enabled)
    Drop-In: /usr/lib/systemd/system/rc-local.service.d
             `-debian.conf
             /etc/systemd/system/rc-local.service.d
             `-ttyoutput.conf
     Active: active (running) since Tue 2023-08-08 14:14:15 BST; 12min ago
    Process: 482 ExecStart=/etc/rc.local start (code=exited, status=0/SUCCESS)
   Main PID: 500 (python3)
      Tasks: 1 (limit: 3933)
        CPU: 1.926s
     CGroup: /system.slice/rc-local.service
             `-500 python3 /home/ubuntu/my_piracer/basic_example.py
```