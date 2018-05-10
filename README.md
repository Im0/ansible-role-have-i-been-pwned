haveibeenpwned Ansible role
===========================

Query the ["Have I been pwned?"](https://haveibeenpwned.com) API for breached accounts (email) or passwords. 

Requirements
------------

Internet access to query the haveibeenpwned API's.

Role Variables
--------------

Required variables for each lookup includes:

| Lookup          |  Variables                                                               |
|-----------------|--------------------------------------------------------------------------|
| password (hash) | `hash`: SHA-1 hashed password. 5 characters will be shared with the API. |
| password        | `password`: Plain text password is SHA-1 hashed locally, 5 chars shared. |
| account_breach  | `account`: The email address to search the API for.

If a password or account are found in either list the task will fail.

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - name: Check have i been pwned
      hosts: localhost
      roles:
      - { role: ansible-role-have-i-been-pwned,
          lookup: 'password',
          password: 'password123' }
      - { role: ansible-role-have-i-been-pwned,
          lookup: 'password',
          hash: 'AB87D24BDC7452E55738DEB5F868E1F16DEA5ACE'}
      - { role: ansible-role-have-i-been-pwned,
          lookup: 'account_breach',
          account: 'test@test.com'}

Alternatively, call the role/task name directly:

    tasks:
      - include_role:
          name: Im0.ansible-role-have-i-been-pwned
          tasks_from: password_lookup
        vars:
          password: 'password123'
      - include_role:
          name: Im0.ansible-role-have-i-been-pwned
          tasks_from: account_breach
        vars:
          account: email@address.com
        
If the password has been breached, or, email address in a data leak the task will fail.

License
-------

GNU General Public License v3.0

See [COPYING](https://github.com/ansible/ansible/blob/devel/COPYING) to see the full text.

Author Information
------------------

John Imison <john+github@imison.net> 
