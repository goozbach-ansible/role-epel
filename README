An Ansible role for the EPEL Yum repositiories.

To use, setup your role like this:

    ---
    - hosts: all
      remote_user: root
      roles:
        - epel

Optionally you can enable `epel-testing` like this:

    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: epel, epel_testing_enabled: 1 }
