# Deploy and Prepare VM Guests
ansible-playbook -i inventory/hosts.ini deploy_pure_kubernetes.yml --ask-pass --ask-become-pass

# Deploy kubernetes using kubespray
ansible-playbook -i inventory/hosts.ini cluster.yml  -b -K


