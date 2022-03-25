


Goal: check the vlan 2) if vlan match in ifconfig output , get the gateway from bknicipsroutes.csv inventory , check the gatwaystatus, create a report, send an email with attachment
run the role based playbook
ansible-playbook -i inv.ev -e role_name=testrole -e role_action=monitor_backup_nic_health_check monitor_backup_nic_health_check_role.yml

what is not working 
- name: "Check {{ bknicipsroutes_file }} for Backup"
  set_fact:
    east1_gateway: "{{ lookup('csvfile', host1 +' file=bknicipsroutes.csv delimiter=, col=2') }}"
    #debug: msg="{{ lookup('csvfile', hostvars[inventory_hostname] + ' ' +' file=bknicipsroutes.csv delimiter=, col=2') }}"
    #east1_gateway: "{{ lookup('csvfile', ansible_hostname ' + ' file=' + bknicipsroutes_file + ' delimiter=, col=2') }}"
    #east1_gateway: "{{ lookup('csvfile', ansible_nodename + '-bak' + ' file=' + bknicipsroutes_file + ' delimiter=,') }}"

- debug: var=east1_gateway

2) add error hadling
3) create a final report using jinga template



