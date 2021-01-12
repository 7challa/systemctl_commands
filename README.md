# Systemctl Commands
### Viewing Systemd Information
```javascript
systemctl list-dependencies : Show a unit’s dependencies
systemctl list-sockets : List sockets and what activates
systemctl list-jobs : View active systemd jobs
systemctl list-unit-files : See unit files and their states
systemctl list-units : Show if units are loaded/active
systemctl get – default : List default target (like run level)
```

### Viewing a service file
```javascript
systemctl cat <service>
Example: systemctl cat haproxy
```
### Working with Services
```javascript
systemctl stop service : Stop a running service
systemctl start service : Start a service
systemctl restart service : Restart a running service
systemctl reload service : Reload all config files in service
systemctl status service : See if service is running/enabled
systemctl enable service : Enable a service to start on boot
systemctl enable service --now : Enable a service to start on boot and start the service NOW
systemctl disable service : Disable service–won’t start at boot
systemctl show service : Show properties of a service (or other unit)
systemctl -H host status network : Run any systemctl command remotely
```
### Changing System States
```javascript
systemctl reboot : Reboot the system (reboot.target)
systemctl poweroff : Power off the system (poweroff.target)
systemctl emergency : Put in emergency mode (emergency.target)
systemctl default : Back to default target (multi-user.target)
```
### Viewing Log Messages
```javascript
journalctl : Show all collected log messages
journalctl -u network.service : See network service messages
journalctl -f : Follow messages as they appear
journalctl -k : Show only kernel messages
```
### SysVinit to Systemd Cheat Sheet
```javascript
Sysvinit: service SERVICE_NAME start
Systemd: systemctl start SERVICE_NAME (Example: systemctl start cron.service)
Notes: Used to start a service (not reboot persistent)
```
### Sysvinit: service SERVICE_NAME stop
```javascript
Systemd: systemctl stop SERVICE_NAME
Notes: Used to stop a service (not reboot persistent)
```
### Sysvinit: service SERVICE_NAME restart
```javascript
Systemd: systemctl restart SERVICE_NAME
Notes: Used to stop and then start a service
```
### Sysvinit: service SERVICE_NAME reload
```javascript
Systemd: systemctl reload SERVICE_NAME
Notes: When supported, reloads the config file without interrupting pending operations.
```
### Sysvinit: service SERVICE_NAME condrestart
```javascript
Systemd: systemctl condrestart SERVICE_NAME
Notes: Restarts if the service is already running.
```
### Sysvinit: service SERVICE_NAME status
```javascript
Systemd: systemctl status SERVICE_NAME
Notes: Tells whether a service is currently running.
```
### Sysvinit: chkconfig SERVICE_NAME on
```javascript
Systemd: systemctl enable SERVICE_NAME
Notes: Turn the service on, for start at next boot, or other trigger.
```
### Sysvinit: chkconfig SERVICE_NAME off
```javascript
Systemd: systemctl disable SERVICE_NAME
Notes: Turn the service off for the next reboot, or any other trigger.
```
### Sysvinit: chkconfig SERVICE_NAME
```javascript
Systemd: systemctl is-enabled SERVICE_NAME
Notes: Used to check whether a service is configured to start or not in the current environment.
```
### Sysvinit: chkconfig –list
```javascript
Systemd: systemctl list-unit-files –type=service (or) ls /etc/systemd/system/*.wants/
Notes: Print a table of services that lists which runlevels each is configured on or off
```
### Sysvinit: chkconfig –list | grep 5:on
```javascript
Systemd: systemctl list-dependencies graphical.target
Notes: Print a table of services that will be started when booting into graphical mode
```
### Sysvinit: chkconfig SERVICE_NAME –list
```javascript
Systemd: ls /etc/systemd/system/*.wants/SERVICE_NAME.service
Notes: Used to list what levels this service is configured on or off
```
### Sysvinit: chkconfig SERVICE_NAME –add
```javascript
Systemd: systemctl daemon-reload
Notes: Used when you create a new service file or modify any configuration
```
### Runlevels to Targets Cheat Sheet
```javascript
Sysvinit: 0
Systemd: runlevel0.target, poweroff.target
Notes: Halt the system.

Sysvinit: 1, s, single
Systemd: runlevel1.target, rescue.target
Notes: Single user mode.

Sysvinit: 2, 4
Systemd: runlevel2.target, runlevel4.target, multi-user.target
Notes: User-defined/Site-specific runlevels. By default, identical to 3.

Sysvinit: 3
Systemd: runlevel3.target, multi-user.target
Notes: Multi-user, non-graphical. Users can usually login via multiple consoles or via the network.

Sysvinit: 5
Systemd: runlevel5.target, graphical.target
Notes: Multi-user, graphical. Usually has all the services of runlevel 3 plus a graphical login.

Sysvinit: 6
Systemd: runlevel6.target, reboot.target
Notes: Reboot

Sysvinit: emergency
Systemd: emergency.target
Notes: Emergency shell
```
### Changing runlevels:
```javascript
Sysvinit: telinit 3
Systemd: systemctl isolate multi-user.target (OR systemctl isolate runlevel3.target OR telinit 3)
Notes: Change to multi-user run level.

Sysvinit: sed s/^id:.*:initdefault:/id:3:initdefault:/
Systemd: ln -sf /lib/systemd/system/multi-user.target /etc/systemd/system/default.target
Notes: Set to use multi-user runlevel on next reboot.
```
