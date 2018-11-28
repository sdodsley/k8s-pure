# Deploy and prepare VM Guests
sudo ansible-playbook -i inventory/hosts.ini deploy_pure_kubernetes.yml --ask-pass --ask-become-pass


