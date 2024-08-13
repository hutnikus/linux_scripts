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

## Gnome extensions
- install gnome extension manager (if not present)
- https://extensions.gnome.org/extension/906/sound-output-device-chooser/

## Firewall
- firewall frontend is called gufw, it is disabled by default on pop_os





