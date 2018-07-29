SSH
===

SSH role manages sshd config file and ssh users keys.

Requirements
------------

All users mus already exist on the system. Also for now only /home/[username] folders are supported.

Role Variables
--------------

#### SSH service:
ssh_managed_ssh: Specifies if SSH configuration file is managed (default: true). Useful if one wants to manage SSH keys only.
ssh_listen_addresses: Specifies SSH listening addresses (default: 0.0.0.0 and ::)
ssh_listen_port: Specifies SSH port (default: 22)
ssh_keys_only: Enables mandatory SSH key usage (default: true)

#### SSH Key management:
ssh_tenants: Dict of tenants example:
```
group1:
	key1
	key2
group2:
	key2
	key3
```
ssh_keys: Dict of public keys
```
key1: "ssh-rsa ... key@host"
key2: ...
key3: ...
```
ssh_users: Data structure specifying which key tenants setup to hosts
```
- { name: user1, keys: [group1, group2] }
...
```

Example Playbook
----------------
```
- hosts: servers
  roles:
  - { role: ssh, ssh_users: [{name: root, keys: [admins, db_managers]}, {name: peter, keys: [peter]}] }
```

License
-------

GPL v3

TODOs
-----

- Support dynamic home folder parameter
- Unit tests
