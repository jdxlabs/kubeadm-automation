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
# Install on Mac
brew install hashicorp/tap/hashicorp-vagrant

# Install on Linux Debian/Ubuntu / WSL2
wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install vagrant

vagrant plugin install virtualbox_WSL2

~/.zshrc
cf. https://developer.hashicorp.com/vagrant/docs/other/wsl
export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"
export VAGRANT_WSL_WINDOWS_ACCESS_USER_HOME_PATH="/home/username/"
export PATH="$PATH:/mnt/c/Program\ Files/Oracle/VirtualBox/"

/etc/wsl.conf
# Enable extra metadata options by default
[automount]
enabled = true
root = /mnt/
options = "metadata,umask=77,fmask=11"
mountFsTab = false

# Restart WSL2
Restart-Service -Name "LxssManager"
```

### Problem for SSH access : chmod doesn't work with Vagrant

Some tips : 
https://stackoverflow.com/questions/29021246/ssh-fails-due-to-key-file-permissions-when-i-try-to-provision-a-vagrant-vm-with
https://thedatabaseme.de/2022/02/20/vagrant-up-running-vagrant-under-wsl2/


Still fails on WSL2, at this step :
```
TASK [Gathering Facts] *********************************************************
Thursday 29 December 2022  23:43:12 +0100 (0:00:00.403)       0:00:00.403 *****
[WARNING]: Unhandled error in Python interpreter discovery for host k8s-master:
Failed to connect to the host via ssh: Connection timed out during banner
exchange  Connection to 172.28.144.1 port 2222 timed out
fatal: [k8s-master]: UNREACHABLE! => {"changed": false, "msg": "Data could not be sent to remote host \"172.28.144.1\". Make sure this host can be reached over ssh: Connection timed out during banner exchange\r\nConnection to 172.28.144.1 port 2222 timed out\r\n", "unreachable": true}

PLAY RECAP *********************************************************************
k8s-master                 : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0

Thursday 29 December 2022  23:44:12 +0100 (0:01:00.327)       0:01:00.731 *****
===============================================================================
Gathering Facts -------------------------------------------------------- 60.33s
Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```
