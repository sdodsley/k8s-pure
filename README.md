# Prepare deployment hosts
## Install Ansible
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt-get install ansible

## Install Halm
sudo snap install helm --classic

# Deploy and Prepare VM Guests
ansible-playbook -i inventory/hosts.ini deploy_pure_kubernetes.yml --ask-pass --ask-become-pass

# Deploy kubernetes using kubespray
ansible-playbook -i inventory/hosts.ini cluster.yml  -b -K


