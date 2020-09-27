# Ansible Role: firewall

An Ansible Role that allows to configure a firewall.

**NOTE**: it does not work on Docker.

**NOTE**: Ansible needs Python3 on Debian.

[![Actions Status](https://github.com/tristan-weil/ansible-role-firewall/workflows/molecule/badge.svg?branch=master)](https://github.com/tristan-weil/ansible-role-firewall/actions)

## Role Variables

Available variables are listed below, (see also `defaults/main.yml`).

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| firewall_sysctl | {{ _firewall_default_sysctl }} | a list of <*firewall_systcl*> |
| firewall_rules | {{ _firewall_default_rules }} | a list of <*firewall_rule*> |
| firewall_whitelist | [] | a list of IPv4 or IPv6 that are whitelisted |
| firewall_sshguard_enabled | True | *True / False*: enabe support for `sshguard` |

### <*firewall_sysctl*>

A *firewall_sysctl* represents a `sysctl` key/value.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| name          | the name of the `sysctl` parameter |
| value         | the value of the `sysctl` parameter |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

### <*firewall_rule*>

A *firewall_rule* represents a firewallD rule.

The variables and the values are the same for all platforms (see `vars/main.yml`).

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| from          | *any / ip[/mask]*: the CIDR of the originating packet |
| port          | the port    |
| proto         | *tcp / udp / icmp / icmp6* : the IP protocol |
| family        | *inet / inet6*: the IP family |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| state         | allow   | *allow / deny*: the action to choose when a packet is matched |
| service       |         | the name of a service (if set other options are not used) | 
| to            |         | *any / ip[/mask]*: the CIDR of the destination packet |
| on            |         | the name of the interface |
| source_port   |         | the source port |

## Example Playbook

    - hosts: 'webservers'
      vars:
        my_custom_rules:
          - port: '80'
            direction: in
            proto: tcp
            family: "{{ _firewall_translations['inet'] }}"
            state: "{{ _firewall_translations['deny'] }}"
            from: "{{ _firewall_translations['any'] }}"
            to: "{{ _firewall_translations['any'] }}"

      roles:
        - role: 'ansible-role-firewall'
          firewall_rules: "{{ firewall_default_rules | union(__firewall_rules) }}"
              
## Todo

None.

## Dependencies

See [requirements_galaxy.yml](https://github.com/tristan-weil/ansible-role-firewall/blob/master/requirements_galaxy.yml)

## Supported platforms

See [meta/main.yml](https://github.com/tristan-weil/ansible-role-firewall/blob/master/meta/main.yml)

## License

See [LICENSE.md](https://github.com/tristan-weil/ansible-role-firewall/blob/master/LICENSE.md)
