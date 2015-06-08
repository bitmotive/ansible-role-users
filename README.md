ansible-role-users
=========

Configure users and groups.

Requirements
------------

This role has been tested on EL6 hosts with Ansible 1.9.1.

Role Variables
--------------

__role\_users\_customize\_skel__: Set to true to add files to the /etc/skel directory before creating users.

__role\_users\_set\_aliases__: Set to true to customize e-mail aliases for users.

__role\_users\_groups__: An array representing groups.

```
role_users_groups:
- {
  name: 'sshers',
  system: 'no'
}
- {
  name: 'www',
  system: 'yes'
}
```

__role\_users\_list: An array of hash items representing users.

```
role_users_list:
- { 
    username: 'john',
    password: 'password',
    email: 'test@example.com',
    groups: 'sshers',
    system: 'no',
    createhome: 'yes'
}
- {
    username: 'jane',
    password: 'password',
    email: 'email@example.com',
    groups: 'www',
    system: 'no',
    createhome: 'yes'
}
```

The "e-mail" value will be used as an alias for the user in /etc/aliases. 

The value for 'password' should be a crypted password as 
[described in the ansible docs](http://docs.ansible.com/faq.html#how-do-i-generate-crypted-passwords-for-the-user-module).

Example of generating crypted passwords with Python3.4:

```
python3.4 -c "from passlib.hash import sha512_crypt; import getpass; print(sha512_crypt.encrypt(getpass.getpass()));"
```

Dependencies
------------

None.

Example Playbook
----------------

```
- hosts: servers
  roles:
    - { role: bitmotive.ansible-role-users, tags: "users,common" }
```

License
-------

MIT
