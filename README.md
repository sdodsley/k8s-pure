# Prepare Deployment Hosts
## Install Ansible
sudo apt-get update <br />
sudo apt-get install software-properties-common <br />
sudo apt-add-repository --yes --update ppa:ansible/ansible <br />
sudo apt-get install ansible <br />

## Install Halm Client
sudo snap install helm --classic

## Pull Kubespray and Copy Content
cd /tmp <br />
git clone https://github.com/kubernetes-sigs/kubespray.git <br />
sudo cp -rf /tmp/kubespray/. /etc/ansible/ <br />
sudo pip install -r requirements.txt <br />

# Deploy and Prepare VM Guests
ansible-playbook -i inventory/hosts.ini deploy_pure_kubernetes.yml --ask-pass --ask-become-pass

# Deploy Kubernetes using Kubespray
ansible-playbook -i inventory/hosts.ini cluster.yml  -b -K


# Complete Post Tasks and install Pure Service Orchestrator
sudo ansible-playbook post_pure_kubernetes.yml -e 'kubeconfig=/etc/ansible/inventory/artifacts/admin.conf' -e 'psoconfig=/etc/ansible/inventory/pso_config.yml'
