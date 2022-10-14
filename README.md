# Combines the OpenScap Scanning utility and Ansible to automate the scanning process and scan result collection.

Consists of 3 main ansible roles

OSv7:
  - Scans RHEL7, CENTOS7, ROCKY7 Operating Systems
  - Determines if the Operating System is a Graphical or CLI and applies the correct profile 

OSv8:  
  - Scans RHEL8, CENTOS8, ROCKY8 Operating Systems
  - Determines if the Operating System is a Graphical or CLI and applies the correct profile 

mozilla:
  - Tested on RHEL CENTOS ROCKY instances  
  - Looks for a Mozilla FireFox instance if found it will conduct a Scan.


Inventory: consist of 3 projects namespaces to incorperate continous compliance and RMF development. ( use or create inventory to match your use case )
  - GDPv3
  - DCWS
  - DDSMv2
  
How to use:

1. ansible-playbook -i ./inventory/gdpv3 OSv7.yml -K
    - call the project or hosts file within the inventory directory using the "-i" flag
    - invoke the privilege escalation for remote hosts with "-K" flag

2. ansible-playbook -i ./inventory/gdpv3 OSv7.yml -K --limit apcn
    - the addition of the "--limit" limits the scanning to a set or group defined within the inventory file

3. 2 reports will be generated at the end of the play and will be dropped in a created oscap-reports ( one directory back ) with matching hostnames.
    - html for easy viewing 
    - view for stigviewer import

notes: 
    - The playbook starts with updating "scap-security-guide" using yum.
    - Adjust the playbooks with the correct path to the roles is cloning on another instanc
    - Ensure ssh keys are shared to correct hosts defined in the inventory file.

To Do's:
    - implement tags for bypass the yum update scap-security-guide if needed.
    - streamline vars and incorperate host/group vars for better structure.
    - import rmf baseline files (playbook) to stig and scan all at once. 
   
