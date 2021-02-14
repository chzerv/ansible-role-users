Ansible Role: Users
=========

![Ansible Molecule](https://github.com/chzerv/ansible-role-users/workflows/Test%20and%20release./badge.svg?branch=master)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Ansible Role](https://img.shields.io/ansible/role/50034?color=dodgerblue)](https://galaxy.ansible.com/chzerv/users)

Ansible role to manage users and groups on Linux systems.

Role Variables
--------------

Below is a list of the role's variables, along with a brief explanation, their default values and their possible values.

``` yaml
users_create_group_per_user: false
```

> Create a group for every user and make it their primary group.
> For example, for the user `foo`, the group `foo` will be created and will be assigned as their primary group.

``` yaml
users_default_group: users
```

> The default group to be used if `users_create_group_per_user` is set to `false`, 

``` yaml
users_default_shell: /bin/bash
```

> The default shell to be used.

```yaml
users_user_list: []
#users_user_list:
#  - name: testUser
#    append: true
#    comment: "Test user"
#    create_home: true
#    home: "/home/testUser"
#    generate_ssh_key: true
#    group: "{{ users_default_group }}"
#    groups: admin,power,storage
#    password: amazing_pwd
#    update_password: always
#    shell: "{{ users_default_shell }}"
#    uid: 1005
#    system: no
#    state: present
#    expires: -1
#    force: false
#    sudo_opts: ALL=(ALL) ALL
```

> A list of users and their desired configuration. Supported values are:
>
> + `username`: The user's username.
> + `append`: **[true|false]** If true, the user is **additionally** added to the groups specified in `groups`. If false, the user is **only** added to the groups specified in `groups`. Defaults to `true`.
> + `comment`: User description.
> + `create_home`: **[true|false]** Whether to create a home directory for the user. Defaults to `true`.
> + `home`: The user's home directory. Defaults to "/home/username".
> + `generate_ssh_key`: **[true|false]** Whether to generate SSH keys for the user.
> + `group`: The user's primary group. Controlled by the `users_default_group` variable.
> + `groups`: Groups the user will be added to.
> + `password`: The user's password. Hashed using `sha512`.
> + `update_password`: **[always|on_create]** If set to `always`, the password will be updated only if it's different than the previous one. If set to `on_create`, the password will be set only for new users. Defaults to `on_create`.
> + `shell`: The user's default shell. Controlled by the `users_default_shell` variable.
> + `uid`: The user's ID (UID).
> + `system`: **[true|false]** Whether this is a system account or not.
> + `state`: **[present|absent]** Whether to create or remove the user. Defaults to `present`.
> + `expires`: An expiry date for the user's account. Setting this value to `-1` will remove the expiry time.
> + `force`: If `state: absent`, directories associated with the user will also be deleted. When used with `generate_ssh_key: true`, existing keys will be overwritten.
> + `sudo_opts`: `sudoers` configuration for the user. 

>> The only required option is `username`. Everything else is optional and should be adjusted according to your needs.

```yaml
users_group_list: []
#users_group_list:
#  - name: group1
#    gid: 985
#    state: present
#    system: false
```

> A list of groups and their desired configuration. Supported values are:
>
> + `name`: The group's name.
> + `gid`: The group's ID (GID).
> + `state`: **[present|absent]** Whether to create or remove the group.
> + `system`: **[true|false]** Whether this is a system group or not.

>> The only required option is `name`. Everything else is optional and should be adjusted according to your needs.

Example Playbook
----------------

```yaml
- hosts: server

  vars_files:
    - vars/main.yml

  roles:
    - { role: chzerv.users }
```

The `vars/main.yml` file:

```yaml
users_group_list:
  - name: testGroup
    gid: 1010

users_user_list:
  - username: foobar
    comment: Test user
    create_home: true
    password: password
    sudo_opts: ALL=(ALL) ALL
    generate_ssh_key: true

  - username: barfoo
    comment: Test user2
    create_home: false
    password: password2
```

License
-------

MIT / BSD

Author Information
------------------

Chris Zervakis
