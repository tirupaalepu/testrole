
Checking Backup NIC status

Goal: Check the vlan 2) If vlan match or exist in ifconfig output , get the gateway from bknicipsroutes.csv inventory , check the gatwaystatus in routing table , create the final report uisng jinga , send an email with attachment

Env: default/main.yml # have var info
  files/bknicipsroutes.csv # network gatway info (3d and 4th)
  tassk/monitor_backup_nic_health_check.yml > task playbook

Run the role based playbook
ansible-playbook -i inv.env -e role_name=testrole -e role_action=monitor_backup_nic_health_check master_test.yml

what is not working and not showing gateway info.
- name: "Check {{ bknicipsroutes_file }} for Backup"
  set_fact:
    #east1_gateway: "{{ lookup('csvfile', host1 +' file=bknicipsroutes.csv delimiter=, col=2') }}"
    east1_gateway: "{{ lookup('csvfile', hostvars[inventory_hostname] + ' ' +' file=bknicipsroutes.csv delimiter=, col=2') }}"
    #east1_gateway: "{{ lookup('csvfile', ansible_hostname ' + ' file=' + bknicipsroutes_file + ' delimiter=, col=2') }}"
    #east1_gateway: "{{ lookup('csvfile', ansible_nodename + '-bak' + ' file=' + bknicipsroutes_file + ' delimiter=,') }}"

- debug: var=east1_gateway

2) Remove ignore_errors: yes nad add error hadling - not adding any error hadling methods 
3) Create a final report using jinga template



