#Configure Network Bonding

 This repository has a virtual machine just to check if the bond is being correctly configured.

 You can find all configurations on ansible/

 1. playbook.yml
 2. templates/bond.j2
 3. hosts file


 To run and test as configurations on the VM, just run or 'vagrant up' for a machine created and configured.

 If you already have a machine installed and want to change some settings, run the 'vagrant provision'.

 To test more elaborate in a production environment, just configure the 'hosts' file and run the playbook on terminal.

 This Test was done only on Ubuntu 18.04.

#Skel - Single
 To more information to the skelet of Vagrantfile and your configs:
  https://github.com/frock81/skel-vagrant-single-machine-dev-env
