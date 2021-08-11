Role Name
=========

This role deploys IBM Spectrum Protect.

Requirements
------------

CentOS Stream/RHEL 8 minimal installation and public key authentication between command host and target machine

Role Variables
--------------

Defaults:
```
mariadb_version:
```

* `mariadb_*` - responsible for MariaDB installation (repository, version, distribution)


Dependencies
------------

N/A

Example Playbook
----------------

This deploys Kodo server on `server` host (only one server can be deployed)
and multiple agents on `agents` hosts

```
- hosts: isp
  roles:
   - xe0nic.ansible_isp
```

Example hosts inventory (you need to make sure that SSH public key authentication for
ansible user provided in inventory is configured):

```
[all:vars]
ansible_user = root

[isp]
192.168.155.233
```

License
-------

MIT

Author Information
------------------

For more information visit product website: https://storware.eu/products/kodo-for-endpoints
Documentation: https://storware.gitbook.io/kodo-for-endpoints