Ansible Role for LT2P
=========

Configures L2TP for use with an IPsec server.

Requirements
------------

## ansible.cfg

This role is designed to work with merge "hash_behaviour". Make sure your
ansible.cfg contains these settings

```INI
[defaults]
hash_behaviour = merge
```

Role Variables
--------------

```YAML
l2tp_packages:
  - xl2tpd
l2tp_config_base: /etc
l2tp_config:
  dns: 8.8.8.8
  mtu: 1410
  mru: 1410
  name: vpn-server
  address: 1.2.3.4
  local_ip: 10.0.0.1
  subnet: 10.0.0.10-10.0.0.255
  users:
    - name: test
      password: 123
      ip: 10.0.0.42
```

Dependencies
------------

None.

Example Playbook
----------------

```YAML
- hosts: servers
  roles:
    - role: l2tp
      vars:
        l2tp_config:
          name: vpn-server
          address: "{{ ansible_default_ipv4.address }}"
          local_ip: 10.0.0.1
          subnet: 10.0.0.10-10.0.0.255
          users:
            - name: test
              password: 123

- hosts: clients
  roles:
    - role: l2tp
      vars:
        l2tp_config:
          name: vpn-server
          address: 1.2.3.4
          local_ip: 10.0.0.1
          subnet: 10.0.0.10-10.0.0.255
          users:
            - name: test
              password: 123
```

License
-------

MIT
