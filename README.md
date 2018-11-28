# Prepare Deployment Hosts
## Required for vSphere Integration with Ansible
sudo apt-get install python-pip python-dev build-essential <br />
pip install --install pyvmomi <br />
sudo pip install -r requirements.txt <br />

## Install Ansible
sudo apt-get update <br />
sudo apt-get install software-properties-common <br />
sudo apt-add-repository --yes --update ppa:ansible/ansible <br />
sudo apt-get install ansible <br />

## Install Helm Client
sudo snap install helm --classic

## Kubespray
Note: Please review kubespray documentation to customise for your deployment <br />
kubespray guide - https://github.com/kubernetes-sigs/kubespray <br /> <br />
git clone https://github.com/kubernetes-sigs/kubespray.git /tmp/kubespray <br />
sudo cp -rf /tmp/kubespray/. /etc/ansible/ <br />

## k8s-pure
git clone https://github.com/dan-pure/k8s-pure.git /tmp/k8s-pure <br />
sudo cp -rf /tmp/k8s-pure/. /etc/ansible/  <br />

# Deploy and Prepare VM Guests
ansible-playbook -i inventory/hosts.ini deploy_pure_kubernetes.yml --ask-pass --ask-become-pass

# Deploy Kubernetes using Kubespray
ansible-playbook -i inventory/hosts.ini --become --become-user=root cluster.yml

# Complete Post Tasks and Install Pure Service Orchestrator
sudo ansible-playbook post_pure_kubernetes.yml -e 'kubeconfig=/etc/ansible/inventory/artifacts/admin.conf' -e 'psoconfig=/etc/ansible/inventory/pso_config.yml'
