# Linux setup notes

The following file contains notes that may or may not be needed depending on the installation or the way the system is installed.
Some notes are here because some external interaction is needed (e.g. moving private files via usb or setting up a dual boot)

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

## Configure screenshot utility
- in the installation script, I have added kde-spectacle, which is as to-the-point as needed
- however, the shortcuts cannot be set programatically, so set them visualy through the program
