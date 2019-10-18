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

##### Complex configuration

```yaml
---
- hosts: all
  roles:
    - systemd
  vars:
```

#### License

MIT

#### Author Information

* Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-systemd/issues)!
