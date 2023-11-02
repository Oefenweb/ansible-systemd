## systemd

[![CI](https://github.com/Oefenweb/ansible-systemd/workflows/CI/badge.svg)](https://github.com/Oefenweb/ansible-systemd/actions?query=workflow%3ACI)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-systemd-blue.svg)](https://galaxy.ansible.com/Oefenweb/systemd)

Manage [systemd](https://www.freedesktop.org/wiki/Software/systemd/) services in Debian-like systems.

#### Requirements

None

#### Variables

* `systemd_etc_bootchart_content`: [default: `''`]: `bootchart.conf` file content
* `systemd_etc_journald_content`: [default: `''`]: `journald.conf` file content
* `systemd_etc_logind_content`: [default: `''`]: `logind.conf` file content
* `systemd_etc_resolved_content`: [default: `''`]: `resolved.conf` file content
* `systemd_etc_system_content`: [default: `''`]: `system.conf` file content
* `systemd_etc_timesyncd_content`: [default: `''`]: `timesyncd.conf` file content
* `systemd_etc_user_content`: [default: `''`]: `user.conf` file content

* `systemd_service_files`: [default: `[]`]: Service file declarations (files in `/etc/systemd`, e.g. `memcached.service`)
* `systemd_service_files.{n}.unit`: [required]: Unit name (e.g. `memcached`)
* `systemd_service_files.{n}.content`: [default: `''`]: Service file content
* `systemd_service_files.{n}.handler_state`: [optional]: The state to be set on changes
* `systemd_service_files.{n}.enabled`: [optional]: Whether the service should start on boot
* `systemd_service_files.{n}.state`: [optional]: The wanted state of the service (e.g. `started`, `stopped`)
* `systemd_service_files.{n}.masked`: [optional]: Whether the service should be masked or not, a masked service is impossible to start

* `systemd_unit_files`: [default: `[]`]: Unit file declarations (files in `/etc/systemd/*.service.d/`, e.g. `limits.conf`)
* `systemd_unit_files.{n}.unit`: [required]: Unit name (e.g. `mysql`)
* `systemd_unit_files.{n}.file`: [required]: `conf` file name (e.g. `limits`)
* `systemd_unit_files.{n}.content`: [default: `''`]: Unit file content
* `systemd_unit_files.{n}.handler_state`: [optional]: The state to be set on changes
* `systemd_unit_files.{n}.enabled`: [optional]: Whether the service should start on boot
* `systemd_unit_files.{n}.state`: [optional]: The wanted state of the service (e.g. `started`, `stopped`)
* `systemd_unit_files.{n}.masked`: [optional]: Whether the unit should be masked or not, a masked unit is impossible to start

## Dependencies

None

#### Example(s)

##### Simple configuration

```yaml
---
- hosts: all
  roles:
    - oefenweb.systemd
```

##### Complex configuration (memcached and mysql)

```yaml
---
- hosts: all
  roles:
    - oefenweb.systemd
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
        handler_state: restarted

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
