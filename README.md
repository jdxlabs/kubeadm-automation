# Kubeadm Automation

Deploy a Kubeadm Kubernetes cluster with Vagrant and Ansible.

Update ``NODE_NETWORK_BASE`` in ``Vagrantfile`` with your network prefix if you have **virtalbox network limitations**.

Deploy the Kubernetes cluster :
```sh
vagrant up
```

Useful commands :
```sh
# to see the current status
cd ./kubeadm-automation
vagrant status

# to access to the kubernetes cli
vagrant ssh k8s-master
alias k=kubectl
k get nodes

# Relaunch the Ansible code (if needed)
vagrant provision  # it executes the file : site.yml
```

Remove the Kubernetes cluter :
```sh
vagrant destroy -f
```

Based on [kubeadm-ansible](https://github.com/kairen/kubeadm-ansible), [ansible-role-ntp](https://github.com/geerlingguy/ansible-role-ntp) and [ansible-role-locale](https://github.com/robertdebock/ansible-role-locale).