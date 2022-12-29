# Troubleshooting


## Virtualbox configuration

Allow the required ranges :
```
/etc/vbox/networks.conf
* 10.0.0.0/8 192.168.0.0/16
* 2001::/64
```


## WSL2

### Vagrant configuration
```
brew install hashicorp/tap/hashicorp-vagrant
vagrant plugin install virtualbox_WSL2

~/.zshrc
cf. https://developer.hashicorp.com/vagrant/docs/other/wsl
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/mnt/c/Users/Jerome\ Devoucoux/dev/git"
```

### Problem for SSH access : chmod doesn't work with Vagrant

https://stackoverflow.com/questions/29021246/ssh-fails-due-to-key-file-permissions-when-i-try-to-provision-a-vagrant-vm-with

