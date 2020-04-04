Before running the Vagrant file with Ansible enabled, you must run the command: 'ansible-galaxy
install -r requirements.yml' from the command-line. This will install the role in the default
ansible location ~/.ansible/roles. You can navigate there to explore. 

Make sure you read the ~/.ansible/roles/geerlingguy.mysql/README.md file for information about
changing the defaults used in setting up mysql. You can override any defaults by adding the 
modified settings to the playbook.yml file located in the same directory as this file.
