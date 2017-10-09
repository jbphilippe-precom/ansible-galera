galera
======

This role configures Galera/MariaDB 10.0 cluster.

Requirements
------------


Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows.

    galera_cluster_name: mycluster
    galera_bind_address: 0.0.0.0
    galera_max_connections: 100
    galera_gcache_size: "1G"
    mariadb_lv: true
    mariadb_vg_name: "vg_vroot"
    mariadb_lv_name: "lv_mysql"
    mariadb_lv_size: "10g"
    mariadb_version: "10.1"
    mariadb_datadir: "/var/lib/mysql"


    #
    # variables in secret.yml
    #
    #User root
    galera_root_password: 1qa2ws3ed

    #User de maintenance debian
    galera_maintenance_password: 1qa2ws3ed

    #User de monitoring
    galera_monitoring_user: "monitoring_user"
    galera_monitoring_user_password: "monitoring_pass"

    #User applicatif
    galera_app_user: "super_user"
    galera_app_user_password: "super_pass"
    galera_app_user_priv: "*.*:ALL,GRANT"


Examples
--------


Dependencies
------------

None


Playbook launch
---------------
      export ANSIBLE_HOST_KEY_CHECKING=False; ansible-playbook -i hosts playbook.yml --ask-vault-pass --ask-pass --ask-become-pass


Example Playbook
----------------

Inventory file "hosts" example:

      [galera]
      fqdn01l.btsys.local galera_cluster_net="192.168.229.ip"
      fqdn02l.btsys.local galera_cluster_net="192.168.229.ip"
      fqdn03l.btsys.local galera_cluster_net="192.168.229.ip"

Playbook

      - hosts: galera
        sudo: yes
        vars_files:
          - secret.yml
        vars:
          - galera_cluster_name: mycluster
          - mariadb_lv_size: "20g"
        roles:
          - role: ansible-galera


License
-------

Author Information
------------------
