# ansible-host
Ansible playbook for a KVM host

Run this as any user with sudo no passwd privileges

```
ANSIBLE_SSHKEY=$(uuidgen -t)
ssh-keygen -f ~/.ssh/$ANSIBLE_SSHKEY -N ""
cat ~/.ssh/$ANSIBLE_SSHKEY.pub >> ~/.ssh/authorized_keys

sudo apt-get update && sudo apt-get -y install ansible libvirt-bin git

echo "[localhost]
localhost ansible_become=true 

[vm]
" > inventory.ini

echo "Host localhost
  IdentityFile ~/.ssh/$ANSIBLE_SSHKEY.pub
" >> ~/.ssh/config

ansible -m ping -i inventory.ini localhost

git clone git@github.com:matfra/ansible-host.git

```

