# Linux setup notes

The following file contains notes that may or may not be needed depending on the installation or the way the system is installed.
Some notes are here because some external interaction is needed (e.g. moving private files via usb or setting up a dual boot)

## Git setup
git config --global user.name myusername
git config --global user.email myemail
git config --global github.user myusername
git config --global github.token mytoken

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
