# Linux setup notes

The following file contains notes that may or may not be needed depending on the installation or the way the system is installed.
Some notes are here because some external interaction is needed (e.g. moving private files via usb or setting up a dual boot)

## Syncthing
at address http://127.0.0.1:8384/ when running by default

## Git setup
git config --global user.name myusername
git config --global user.email myemail
git config --global github.user myusername
git config --global github.token mytoken

use ssh-keygen to create a key, then add it to profile
use only ssh repo links to clone

## Firefox setup
copy profile root directory from old system to new

## Zsh setup
~~~bash
if command -v curl >/dev/null 2>&1; then
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/romkatv/zsh4humans/v5/install)"
else
  sh -c "$(wget -O- https://raw.githubusercontent.com/romkatv/zsh4humans/v5/install)"
fi
~~~
- create link to .zshrc from this repo `ln -s script_folder/.zshrc ~/.zshrc`


## Gnome extensions
- install gnome extension manager (if not present)
- https://extensions.gnome.org/extension/906/sound-output-device-chooser/

## Firewall
- firewall frontend is called gufw, it is disabled by default on pop_os

## Resolv
- while using pihole and whatnot I disabled systemd-resolved
- I also removed symlink /etc/resolv.conf -> /run/systemd/resolve/stub-resolv.conf
- to bring it back, I have to create the symlink and reenable the service

## Default editor
- `sudo update-alternatives --config editor`
- opens interactive menu

## Hibernate
create a swap partition, should be a bit bigger then the actual RAM.
why even encrypt the thing? 

```bash
sudo swapoff -a
sudo cryptsetyp luksClose cryptswap

sudo cruptsetup luksErase /dev/nvme0n1p2 #if correct partition name
sudo mkswap /dev/ncme0n1p2
sudo swapon /dev/nvme0n1p2

swapon --show # check if on

#get UUID
blkid | grep nvme0n1p2

sudo nvim /etc/kernelstub/configuration
# add "resume=UUID=actual_uuid_that_you_get" to "kernel_options"
sudo kernelstub -v

sudo nvim /etc/initramfs-tools/conf.d/resume
# add RESUME=UUID=your-new-swap-uuid

sudo update-initramfs -u -k all


sudo nano /etc/fstab
# replace /dev/mapper/cryptswap  none  swap  defaults  0  0 with
UUID=your-new-swap-uuid none swap sw 0 0

sudo swapoff -a
sudo swapon -a

# try this
sudo reboot
sudo systemctl hibernate
```

### Bind power button
create script to hibernate

```bash
sudo nano /usr/local/bin/power-button-action.sh
```

add this
```bash
#!/bin/bash
systemctl hibernate

```

continue with this
```bash
sudo chmod +x /usr/local/bin/power-button-action.sh

acpi_listen
# power button press should give line starting with button/power

sudo nano /etc/acpi/events/powerbutton

## add these lines to this
event=button/power
action=/usr/local/bin/power-button-action.sh


sudo systemctl restart acpid

```

now system should hibernate on power button press

## Wayland
to enable wayland on pop_os, you need to edit `/etc/gdm3/custom.conf` and change WaylandEnable=true
then restart the service `sudo systemctl restart gdm3`

-> to get rid of phantom windows, disable the "desktop icons" extension in extension manager
