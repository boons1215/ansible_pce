# 1. First of all, you need to modify the hosts (inventory) file. Update the IP of each nodes and include the hostname FQDN (no domain name is required) under "allnodes" group.
  - For 2x2 PCE cluster, you have to update IP under groups - "core0", "core1", "data0", "data1". Leave "core2" and "core3" empty. 

  - For 4x2 PCE cluster, you have to update IP under groups - "allnodes", "core2", "core3".


# 2. Download the PCE softwares and put under the following directories:
- For new cluster setup, put the following under pce-build/files directory:
  - PCE RPM
  - PCE-UI RPM
  - VEN Bundle tar
  - Release compatibility tar
  - Root and Intermediate CA certs 
  - Server bundle certs and private key 

- For upgrade cluster, put the following under pce-upgrade/files directories:
  - Targetted PCE RPM
  - Targetted PCE-UI RPM
  - Targetted VEN Bundle tar
  - Latest release compatibility tar


# 3. Update the var files accordingly:
- For new cluster setup, update "setup-vars.yml" file.
- For upgrade cluster, update "upgrade-vars.yml" file.


# 4. Command sample:
- For Uninstall PCE
Eg:
  - With SSH Private Key: 
    - ansible-playbook -i hosts pce-remove/site.yml -u centos --private-key wwest-default

  - With SSH Keyless: 
    - ansible-playbook -i hosts pce-remove/site.yml -u centos

- For Setup PCE Cluster
Eg:
  - With SSH Private Key: 
    - ansible-playbook -i hosts pce-build/site.yml -u centos --private-key wwest-default -e "@setup-vars.yml"

- For Upgrade PCE Cluster
Eg:
  - With SSH Private Key: 
    - ansible-playbook -i hosts pce-build/site.yml -u centos --private-key wwest-default -e "@upgrade-vars.yml"
    

# 5. In progress....
- PCE expansion from 2x2 to 4x2
- PCE rollback/downgrade
- PCE split cluster handling when core0 and data0, promoting core1 and data1 as standalone cluster
- PCE restore from backup
- PCE data mastership failover
- PCE switch listen-only mode

