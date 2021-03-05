# Ansible Role: Proxy

[![ubuntu-18](https://img.shields.io/badge/ubuntu-18.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![ubuntu-20](https://img.shields.io/badge/ubuntu-20.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg?style=flat)](https://opensource.org/licenses/MIT)
[![GitHub issues](https://img.shields.io/github/issues/OnkelDom/ansible-role-kexec?style=flat)](https://github.com/OnkelDom/ansible-role-kexec/issues)

## Description

Install and configure proxy applications

* Squid
* SquidGuard
* Dante Socks
* Proxy Pac/Wpad File
* Caddy Webserver

## Requirements

- Ansible >= 2.5 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `proxy_env` | {} | Set proxy environment |

## Example

```yaml
---
- hosts: all
  roles:
  - ansible-role-proxy
  vars:
    sockd_access_rules:
      - name: "Allow any dst"
        src:
          - 10.100.0.2 # boss01.loca.lan
      - name: "Empty Logging for this"
        log: "" # with this, logging is disabled
        src:
          - 10.100.0.101 # test01.loca.lan
          - 10.100.0.102 # test02.loca.lan
        dst:
          - 173.249.21.102/32
      - name: "Other with multiple destinations"
        src:
          - 10.100.1.212 # test04.loca.lan
          - 10.100.1.30  # test06.loca.lane
          - 10.100.1.16  # test08.loca.lan
        dst:
          - 173.249.21.102/32
          - .github.com
          - .githubusercontent.com
          - .stackoverflow.com
```

### Playbook

```yaml
---
- hosts: all
  roles:
  - ansible-role-proxy
```

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
