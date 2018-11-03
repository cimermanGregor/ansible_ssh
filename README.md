SSH
===

SSH role manages sshd config file and ssh users keys.

Requirements
------------

All managed users will be added to the system. Only /home/[username] folders are supported.

Role Variables
--------------

#### SSH service:

* `ssh_managed_ssh`: Specifies if SSH configuration file is managed (default: true). Useful if one wants to manage SSH keys only.
* `ssh_listen_addresses`: Specifies SSH listening addresses (default: 0.0.0.0 and ::)
* `ssh_listen_port`: Specifies SSH port (default: 22)
* `ssh_key_only_auth`: Enable key only authentication (default: true)
* `ssh_banner`: Set custom welcome banner (default: true)
* `ssh_disable_update_motd`: Disables default debian welcome motd (default: false)


#### SSH Key management:
`ssh_users`: Dict of users and used keys example:
```
ssh_users:
  root:
    - user1_key1
  user1:
    - user1_key1
    - user1_key2
  user2:
    - user2
```
`ssh_keys`: Dict of public keys
```
user1_key1: "ssh-rsa ... key@host"
user1_key2: ...
user2: ...
```

Example Playbook
----------------
```
- hosts: servers
  roles:
  - { role: ssh, ssh_users: [{peter: [peter]}], ssh_keys: {peter: "ssh-rsa ..."} }
```

License
-------

GPL v3

TODOs
-----

- Support dynamic home folder parameter
- Unit tests
