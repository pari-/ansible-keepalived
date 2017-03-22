# keepalived

An Ansible role which installs and configures keepalived

<!-- toc -->

- [Requirements](#requirements)
- [Example](#example)
- [Variables](#variables)
  * [Role Variables](#role-variables)
  * [Role Internals](#role-internals)
- [Dependencies](#dependencies)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

## Requirements

Currently this role is developed for and tested on Debian GNU/Linux (release: jessie). It is assumed to work on other Debian distributions as well.

Ansible version in use for development: 2.2.1

## Example

```yaml
- hosts: keepalived-master

  vars:
    keepalived_vrrp_instances:
    - name: "V_I"
      state: "MASTER"
      interface: "eth0"
      virtual_router_id: 42
      priority: 100
      advert_int: 1
      auth_pass: "verySafeAuthPass1"
      vip_list:
      - 192.168.0.100

  roles: 
    - "ansible-keepalived"
```

```yaml
- hosts: keepalived-backup

  vars:
    keepalived_vrrp_instances:
    - name: "V_I"
      state: "BACKUP"
      interface: "eth0"
      virtual_router_id: 42
      priority: 100
      advert_int: 1
      auth_pass: "verySafeAuthPass1"
      vip_list:
      - 192.168.0.100

  roles: 
    - "ansible-keepalived"
```

## Variables

Available variables are listed below, along with default values (see defaults/main.yml). They're generally prefixed with `keepalived_` (which I deliberately leave out here for better formatting).

### Role Variables

variable | default | notes
-------- | ------- | -----
`vrrp_instances` | `` | `A list of VRRP instances`
`vrrp_instance['name']` | `` | `Name of the VRRP instance`
`vrrp_instance['state']` | `` | `State of the VRRP instance`
`vrrp_instance['interface']` | `` | `Network interface of the VRRP instance`
`vrrp_instance['virtual_router_id']` | `` | `Specify which VRRP router id the instance belongs to`
`vrrp_instance['priority']` | `` | `The priority of the VRRP instance`
`vrrp_instance['advert_int']` | `` | `The advertisement interval in seconds of the VRRP instance`
`vrrp_instance['auth_pass']` | `` | `The authentication password of the VRRP instance`
`vrrp_instance['vip_list']` | `` | `A list of virtual IPs of the VRRP instance`
`ip_nonlocal_bind` | `True` | `Allows processes to bind() to non-local IP addresses`

### Role Internals

variable | default | notes
-------- | ------- | -----
`cache_valid_time` | `3600` | `Update the apt cache if its older than the set value (in seconds)`
`keepalived_config_file` | `/etc/keepalived/keepalived.conf` | `Absolute path to keepalived's configuration file`
`default_release` | `jessie` | `The default release to install packages from.`
`package_list` | `['keepalived']` | `The list of packages to be installed`
`packages_state` | `present` | `TBD`
`repo_list` | `['deb http://ftp.debian.org/debian jessie-backports main']` | `TBD`
`repo_state` | `present` | `TBD`
`service_name` | `keepalived` | `TBD`
`supported_distro_list` | `['jessie']` | `A list of distribution releases this role supports`
`update_cache` | `yes` | `Run the equivalent of apt-get update before the operation`


## Dependencies

None

## License

MIT

## Author Information

* Patrick Ringl
