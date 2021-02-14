Ansible Role: Users
=========

Ansible role to manage users and groups on Linux systems.

Requirements
------------

None.

Role Variables
--------------

# WIP

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: server

  vars_files:
    - vars/main.yml

  roles:
    - { role: username.rolename, x: 42 }
```

The `vars/main.yml` file:

```yaml
```

License
-------

MIT / BSD

Author Information
------------------

Chris Zervakis
