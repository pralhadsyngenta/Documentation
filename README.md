# Setting up Development Environment

## 1. Pre-requisites
* Step One
* Step two
* Step three

## 2. Steps
### 2.1 Installing VirtualBox
Reference URL - https://help.ubuntu.com/community/VirtualBox/Installation
Commands:

``` sudo sh -c "echo 'deb http://download.virtualbox.org/virtualbox/debian '$(lsb_release -cs)' contrib non-free' > /etc/apt/sources.list.d/virtualbox.list" && wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -O- | sudo apt-key add - && sudo apt-get update && sudo apt-get install virtualbox-5.0 ```

Please note: above command is a single command and needs to be executed in single attempt.

### 2.2 Installing Vagrant
* Reference URL - https://www.vagrantup.com/downloads.html
* Donload appropriate 32bit or 64bit installation for Ubuntu. You can get this package from other team members.
* You can open the downloaded file with "Ubuntu Software Update center"
* If installing through Ubunntu Software Update Center" then no other command is needed.
