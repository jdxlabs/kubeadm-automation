# Troubleshooting

## Virtualbox configuration

Allow the required ranges :
```
/etc/vbox/networks.conf
* 10.0.0.0/8 192.168.0.0/16
* 2001::/64
```

## Install on Mac
```
brew install hashicorp/tap/hashicorp-vagrant
```

## Install on Windows, with WSL2

```
# Install commands for Vagrant on a Linux Debian/Ubuntu distro :
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant

# Then, there is a plugin for Vagrant :
vagrant plugin install virtualbox_WSL2

~/.zshrc
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"

/etc/wsl.conf
[automount]
options = "metadata"
```

### Some sources for troubleshooting : 
https://developer.hashicorp.com/vagrant/docs/other/wsl
https://stackoverflow.com/questions/29021246/ssh-fails-due-to-key-file-permissions-when-i-try-to-provision-a-vagrant-vm-with
https://thedatabaseme.de/2022/02/20/vagrant-up-running-vagrant-under-wsl2/
https://github.com/geerlingguy/ansible-for-devops/issues/291
https://github.com/JeffReeves/WSL-Ansible-Vagrant-VirtualBox
