# Prepare Deployment Hosts
## Install Ansible
sudo apt-get update <br />
sudo apt-get install software-properties-common <br />
sudo apt-add-repository --yes --update ppa:ansible/ansible <br />
sudo apt-get install ansible <br />

## Install Halm
sudo snap install helm --classic

# Deploy and Prepare VM Guests
ansible-playbook -i inventory/hosts.ini deploy_pure_kubernetes.yml --ask-pass --ask-become-pass

# Deploy Kubernetes using Kubespray
ansible-playbook -i inventory/hosts.ini cluster.yml  -b -K


