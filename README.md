## systemd

[![Build Status](https://travis-ci.org/Oefenweb/ansible-systemd.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-systemd)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-systemd-blue.svg)](https://galaxy.ansible.com/Oefenweb/systemd)

Manage systemd services in Debian-like systems.

#### Requirements

None

#### Variables

None

## Dependencies

None

#### Example(s)

##### Simple configuration

```yaml
---
- hosts: all
  roles:
    - systemd
```

##### Complex configuration (memcached and mysql)

```yaml
---
- hosts: all
  roles:
    - systemd
  vars:
    systemd_service_files:
      - unit: memcached
        content: |
          [Unit]
          Description=Start up memcached, a high-performance memory caching daemon
          After=network.target

          [Service]
          ExecStartPre=/usr/bin/test -x /usr/bin/memcached
          ExecStartPre=/usr/share/memcached/scripts/start-memcached
          ExecStartPre=/usr/bin/install -d -o memcache -g root -m 0775 /run/memcached
          ExecStart=/usr/share/memcached/scripts/systemd-memcached-wrapper /etc/memcached.conf

          [Install]
          WantedBy=multi-user.target
        state: reloaded

    systemd_unit_files:
      - unit: mysql
        file: limits
        content: |
          [Service]
          LimitNOFILE=infinity
          LimitMEMLOCK=infinity
          OOMScoreAdjust=-600
```

#### License

MIT

#### Author Information

* Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-systemd/issues)!
