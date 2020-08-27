# Virtual Box Setup

### Step 1: Install VBox Guest Utils

*Note: This install **must** be of the same version as the Virtual Box Installed Version*

The best way is to attach the iso and start installing. 

### Step 2: Check installation

Once installation is done

`ps -aux | grep vbox -I`

The following should be running

`/usr/bin/VBoxService -f`

`/usr/bin/VBoxClient --vmsvga`

`/usr/bin/VBoxClient --vmsvga`

`/usr/bin/VBoxClient --clipboard`

`/usr/bin/VBoxClient --clipboard`

`/usr/bin/VBoxClient --display`

`/usr/bin/VBoxClient --display`

`/usr/bin/VBoxClient --seamless`

`/usr/bin/VBoxClient --seamless`

`/usr/bin/VBoxClient --draganddrop`


`vmsvga` - should be running to bring the screen to full resolution

### Step 3: Speed up the system startup

 Disable the below services, they are not needed on all startups

`sudo systemctl disable vboxadd-service.service`

`sudo systemctl disable vboxadd.service`

*Note:*

 *These are used to reinstall kernel module on startup and shutdown*

*So, if you change the kernel, start them manually again*

 

Since the other services are disabled, we have to enable `/usr/lib/systemd/system/vboxservice.service` manually

`sudo systemctl enable vboxservice.service`

### Step 4: Start missing client service with ExecStartPost

 In my case, vmsvga was not starting automatically, so I call it additionally.                                              

`[Unit]`

`Description=VirtualBox Guest Service`

`ConditionVirtualization=oracle`

`[Service]`

`ExecStartPre=-/usr/bin/modprobe vboxguest`

`ExecStartPre=-/usr/bin/modprobe vboxvideo`

`ExecStartPre=-/usr/bin/modprobe vboxsf`

`ExecStart=/usr/bin/VBoxService -f`

`ExecStartPost=/usr/bin/VBoxClient --vmsvga` 

`[Install]`

`WantedBy=multi-user.target`



