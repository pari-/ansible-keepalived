# keepalived

[![Build Status](https://travis-ci.org/pari-/ansible-keepalived.svg?branch=master)](https://travis-ci.org/pari-/ansible-keepalived)

An Ansible role which installs and configures keepalived

<!-- toc -->

## Requirements

Currently this role is developed for and tested on Debian GNU/Linux (release: stretch). It is assumed to work on other Debian distributions as well.

Ansible version compatibility:

- __2.3.2.0__ (current version in use for development of this role) 
- 2.2.3.0
- 2.1.6.0
- 2.0.2.0

## Example

```yaml
---

- hosts: "all"
  vars:
    keepalived_vrrp_instance_list:
      - name: "V_I"
        state: "MASTER"
        interface: "{{ ansible_default_ipv4['interface'] }}"
        virtual_router_id: 42
        priority: 100
        advert_int: 1
        auth_pass: "Li+J9sae"
        vip_list:
          - "192.168.0.100"
  roles:
    - role: "ansible-keepalived"
      tags:
        - "keepalived"

```

## Role Variables

Available variables are listed below, along with default values (see defaults/main.yml). They're generally prefixed with `keepalived_` (which I deliberately leave out here for better formatting).

variable | default | notes
-------- | ------- | -----
`cache_valid_time` | `3600` | `Update the apt cache if its older than the set value (in seconds)`
`config_file` | `/etc/keepalived/keepalived.conf` | `Absolute path to keepalived's configuration file`
`default_release` | `{{ ansible_distribution_release\|lower }}` | `The default release to install packages from`
`ip_nonlocal_bind` | `True`| `Allows processes to bind() to non-local IP addresses`
`package_list` | `['keepalived']` | `The list of packages to be installed`
`pre_default_release` | `{{ keepalived_default_release }}` | `The default release to install packages (pre_package_list) from`
`pre_package_list` | `['apt-transport-https','ca-certificates']` | `The list of prerequisite packages to be installed`
`repo_list` | `[]` | `(additional) repository list`
`service_name` | `keepalived` | `Name of the (keepalived) service`
`supported_distro_list` | `['jessie', 'stretch']` | `A list of distribution releases this role supports`
`update_cache` | `yes` | `Run the equivalent of apt-get update before the operation`
`vrrp_instance_list` | `[]` | `A list of keepalived VRRP instances`

## Dependencies

None

## License

MIT

## Author Information

* Patrick Ringl
