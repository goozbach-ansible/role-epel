An Ansible role for the EPEL Yum repositiories.

# Usage

To use, setup your role like this:

```yaml
    ---
    - hosts: all
      remote_user: root
      roles:
        - goozbach.EPEL
```

# Options

## Disabling repos

Enable or disable `epel-testing` or `epel` repositories like this:

-  `epel_testing_enabled` is `0` by default
-  `epel_enabled` is `1` by default

```yaml
    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: goozbach.EPEL, epel_testing_enabled: 1 }
        - { role: goozbach.EPEL, epel_enabled: 0 }
```

To use a disabled repo using the `yum` module use this syntax:

    - name: install the latest version of Apache from the testing repo
      yum: name=httpd enablerepo=epel state=installed

## EPEL Release mode
Change state of `epel-release` rpm (default is `installed`, change to `latest` to get an updated rpm):

```yaml
    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: goozbach.EPEL, epel_state: latest }
```

## Overriding EPEL repository location
*New in `v1.0.0`*

You can now control where your EPEL repository URL points.

There are two different ways you can specify the URL.
However, you must modify the default `use_baseurl` and set it to `True` for either method to work.

### Overriding EPEL repository host and path
Overriding *JUST* the path, hostname, or protocol of your EPEL URLs.

The `baseurl` parameter for each of the defined repositories ( epel, epel-debug, epel-SRPMS, epel-testing, epel-testing-debug, epel-testing-SRPMS ) is generated from the following variables:

- `epel-protocol` -- Changes the `protocol` part of the URL. (default `http://`)
- `epel_urlhost` -- Changes the `host` part of the URL. (default `download.fedoraproject.org`)
- `epel-testing_urlpath` -- Changes the `path` part of the `epel-testing` baseurl. (default `/pub/epel/testing/{{ ansible_distribution_major_version }}/$basearch`)

*NOTE:* change the specifed variables for *EACH* of the repositories you wish to use:

- `epel_urlpath`y
- `epel-debug_urlpath`y
- `epel-srpms_urlpath`y
- `epel-testing_urlpath`y
- `epel-testing-debug_urlpath`y
- `epel-testing-srpms_urlpath`y

### Specifiying an exact URL for EPEL repository
Instead of using a generated URL for the `baseurl` parameter you can specify the entire thing, by setting one of these variables:

- `epel_baseurl`
- `epel-debug_baseurl`
- `epel-srpms_baseurl`
- `epel-testing_baseurl`
- `epel-testing-debug_baseurl`
- `epel-testing-srpms_baseurl`

### Overriding examples

#### Changing just the hostname 

```yaml
    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: goozbach.EPEL, epel_state: latest, use_baseurl: True, epel_urlhost: internal-mirror.example.com}
```

#### Changing hostname and path

```yaml
    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: goozbach.EPEL, epel_state: latest, use_baseurl: True, epel_urlhost: mirror.xmission.com, epel_urlpath: /fedora-epel/6/x86_64/}
```

#### Changing entire url

```yaml
    ---
    - hosts: all
      remote_user: root
      roles:
        - { role: goozbach.EPEL, epel_state: latest, use_baseurl: True, epel_baseurl: 'http://foo.example.com/some/weird/layout/7/$basearch'}
```
