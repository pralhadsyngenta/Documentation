# Setting up Development Environment on Local Machine

## 1. Pre-requisites
* Base operating system must be Ubuntu 14.04. These steps can also be used on CentOS, RHEL and iOS with little changes.
* VT-X option needs to be enabled from hardware Bios settings.
* In case VMWare Workstation is being used then VT-X option needs to be enabled in Processor settings of the particular VM instance as well.

## 2. Steps
### 2.1 Installing VirtualBox
Reference URL - https://help.ubuntu.com/community/VirtualBox/Installation
Commands:

``` 
sudo sh -c "echo 'deb http://download.virtualbox.org/virtualbox/debian '$(lsb_release -cs)' contrib non-free' > /etc/apt/sources.list.d/virtualbox.list" && wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -O- | sudo apt-key add - && sudo apt-get update && sudo apt-get install virtualbox-5.0 
```

Please note: above command is a single command and needs to be executed in single attempt.

### 2.2 Installing Vagrant
* Reference URL - https://www.vagrantup.com/downloads.html
* Donload appropriate 32bit or 64bit installation for Ubuntu. You can get this package from other team members.
* You can open the downloaded file with "Ubuntu Software Update center"
* If installing through Ubunntu Software Update Center" then no other command is needed.

### 2.3 Installing Vagrant's host-updater plugin
Commands:
```
vagrant plugin install vagrant-hostsupdater
```
This plugin is very important in updating the domains names to Guest OS's 'hosts' file. Without this domain name entries needs be added manually.

### 2.4 Install Curl
Reference URL - http://askubuntu.com/questions/9293/how-do-i-install-curl-in-php5 
Commands:
```
sudo apt-get install curl
```
Used for package download/installtion.

### 2.5 Install PHP-Cli
Reference URL - https://ubuntu.flowconsult.at/en/php-command-line-cli-installation
Commands:
```
sudo apt-get install php5-cli
```
### 2.6 Installing NFS
Reference URL - https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-14-04
Commands:
```
sudo apt-get update
sudo apt-get install nfs-kernel-server
sudo apt-get install nfs-common
```
NFS will SYNC the Source-Code directory between Guest and Host machines.

### 2.7 Install composer
Reference URL - https://www.digitalocean.com/community/tutorials/how-to-install-and-use-composer-on-ubuntu-14-04
Commands:
```
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```
In case above command doesn't work then download it from https://getcomposer.org/installer. Go to the folder where this file is downloaded and fire the command-
Command:
```
sudo php installer
```
### 2.8 Install PHP-Curl
Commands:
```
sudo apt-get install php5-curl
```
This is required to run 'composer' commands. Otherwise there will be problems downloading the libs/packages mentioned in 'composer.json'.

### VM Setup

### 2.9 Add public key to your GitHub account
Reference URL - https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key
* Follow only [Generating a new SSH key] section. 
* Once key is created then just add that to your GitHub account unders settings.
* Once done, you wont need credentials to clone (or any other operation) on GitHub repository. 

### 2.10 Clone code-repo on local machine
Commands:
```
git clone https://github.com/repo
```
This assumes you cloned the repo in your home dir `[/home/username/drupalvm]`

### 2.11 Run 'composer install'
Commands:
```
cd syngenta
composer install
./task.sh setup:git-hooks
```
### 2.12 PHP 5.6 changes to config.yml
Reference URL - http://docs.drupalvm.com/en/latest/other/php-56/#ubuntu-1404 
* Make necessary changes to 'box/config.yml' as mentioned on the url above.
* This step is required only because of the conflict in Ansible Roles & Packages.
* Once this issue is resolved then this step will no longer be required. 

### 2.13 Vagrant up
Go inside `[drupalvm]`
Commands:
```
cd drupalvm
vagrant up
```
This command will download and install Ansibles roles and the packages.

### 2.14 SSH to newly created VM
Commands:
```
vagrant ssh
```
### 2.15 Change php.ini settings
Increase the values for Memory Limit, Max Exec Time and Max Input Time @ `[/etc/php5/apache2/php.ini]`. These settings will be specific to local machine only. These settings may vary based on the RESOURCES alloted for VM.
```
max_execution_time = 180
max_input_time = 180
memory_limit = 256M
```
Without these changes DRUSH commands might fail as those are quite heavy on resource consumption.

### 2.16 Synced folders
* Base Operating System: `[home/[user-name]/Sites/drupalvm]`
* VirtualBox Instance: `[/var/www/drupalvm]`
