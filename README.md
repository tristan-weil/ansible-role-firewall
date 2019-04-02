# Ansible Role: firewall

An Ansible role that wraps the distribution/OS specific firewall installation role for Debian and OpenBSD.

## Role Variables

Available common variables are listed below, along with default values (see `defaults/main.yml`):

    firewall_ipv4_block_allcast: True        # block all *cast packets
    
If all multicast, broadcast, anycast should be blocked, leave this variable `True`.

    firewall_ipv4_whitelist: []              # a list of whitelisted IPv4 addresses
    firewall_ipv6_whitelist: []              # a list of whitelisted IPv6 addresses    
    firewall_ipv4_blacklist: []              # a list of blacklisted IPv4 addresses
    firewall_ipv6_blacklist: []              # a list of blacklisted IPv6 addresses
    
The lists of blacklisted IP addresses.
    
    firewall_ssh_port: 22                    # the port of the SSH server
    
Because the access to a remote machine need to be secured, the SSH port must be let open. 
    
For specific variables, see the distrib role.

## Dependencies

None.

## Example Playbook

None (see distrib role).
              
## Todo

Make it available for OpenBSD.

## License

```
Copyright (c) 2018, 2019 Tristan Weil <titou@lab.t18s.fr>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```
