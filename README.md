An Ansible role for the EPEL Yum repositiories.

# Usage

To use, setup your role like this:

    ---
    - hosts: all
      remote_user: root
      roles:
        - epel

# Options

* Enable `epel-testing` like this (default is `0`):

    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: epel, epel_testing_enabled: 1 }

* Change state of `epel-release` rpm (default is `installed`, change to `latest` to get an updated rpm):

    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: epel, epel_state: latest }
