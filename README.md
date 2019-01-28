# Ansible Role for tinc VPN

This is a ansible role for setting up a (single) tinc VPN (https://www.tinc-vpn.org/) on your hosts.

## Usage

Add role to your `requirements.yml`:
```yaml
- src: https://github.com/MatthiasLohr/
  name: mlohr.tincvpn
  version: v0.1.0
```

Set `tincvpn_ip` for your hosts in inventory file:
```ini
[all]
node1 tincvpn_ip=192.168.255.1
node2 tincvpn_ip=192.168.255.2
node3 tincvpn_ip=192.168.255.3
```

Simple playbook example:
```yaml
- hosts: localhost
  roles:
    - mlohr.tincvpn
```


## Host Variables

| Variable Name | Default Value | Description                                                       |
|---------------|---------------|-------------------------------------------------------------------|
| `tincvpn_ip`  | `none`        | tinc IP address of this node (should be part of `tincvpn_subnet`) |


## Role Variables

| Variable Name             | Default Value                         | Description                                                                                           |
|---------------------------|---------------------------------------|-------------------------------------------------------------------------------------------------------|
| `tincvpn_network`         | `"default"`                           | name of the tinc network (e.g. tinc configuration folder name)                                        |
| `tincvpn_interface`       | `"tinc"`                              | name for the network interface used by tinc                                                           |
| `tincvpn_subnet`          | `"192.168.255.0/24"`                  | subnet used by tinc                                                                                   |
| `tincvpn_mode`            | `"switch"`                            | tinc `Mode` setting                                                                                   |
| `tincvpn_hosts`           | `[]`                                  | additional tinc hosts available (not covered by playbook, read [Additional Hosts](#additional-hosts)) |
| `tincvpn_key_bits`        | `2048`                                | private key length                                                                                    |
| `tincvpn_connect_to`      | `[]`                                  | nodes to connect to by default                                                                        |
| `tincvpn_local_directory` | `"{{ inventory_dir }}/tincvpn-hosts"` | where to save host public keys locally                                                                |
