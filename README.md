# Ansible Role for tinc VPN

This is a ansible role for setting up a (single) tinc VPN (https://www.tinc-vpn.org/) on your hosts.

## Usage

Add role to your `requirements.yml`:
```yaml
- src: https://github.com/MatthiasLohr/ansible-role-tincvpn
  name: matthiaslohr.tincvpn
  version: v0.3.0
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
    - matthiaslohr.tincvpn
```


## Host Variables

| Variable Name | Default Value | Description                                                       |
|---------------|---------------|-------------------------------------------------------------------|
| `tincvpn_ip`  | `none`        | tinc IP address of this node (should be part of `tincvpn_subnet`) |


## Role Variables

| Variable Name | Default Value | Description |
|---------------|---------------|-------------|
| `tincvpn_network` | `"default"` | Name of the tinc network (e.g. tinc configuration folder name). |
| `tincvpn_interface` | `"tinc"` | Name for the network interface used by tinc. |
| `tincvpn_subnet` | `"192.168.255.0/24"` | Subnet used by tinc. |
| `tincvpn_mode` | `"switch"` | Tinc `Mode` setting. |
| `tincvpn_extra_hosts` | `[]` | Additional tinc hosts available (not covered by playbook, read [Additional Hosts](#additional-hosts)). |
| `tincvpn_key_bits` | `2048` | Length of RSA private key. |
| `tincvpn_connect_to` | `[]` | Nodes to connect to by default. You can give a single nodename as string or multiple nodes as list of strings. |
| `tincvpn_routes` | `[]` | Add routes using the tinc VPN network interface. |
| `tincvpn_local_directory` | `"{{ inventory_dir }}/tincvpn-hosts"` | Where to save host public keys locally. |


## Configuration Tweaks

### Additional Hosts

In case you want to connect to a node that is not included in the Ansible inventory (e.g. a central router you want to connect to), it is possible to configure additional hosts via playbook variables:
```yaml
tincvpn_extra_hosts:
  - name: externalnode1
    address: externalnode1.example.com
    public_key: |
      -----BEGIN RSA PUBLIC KEY-----
      ...
      -----END RSA PUBLIC KEY-----

  - name: externalnode2
    address: externalnode2.example.com
    public_key: |
      -----BEGIN RSA PUBLIC KEY-----
      ...
      -----END RSA PUBLIC KEY-----
```


### Custom Routes

```yaml
tincvpn_routes:
  - network: "192.168.254.0/24"
    gateway: "192.168.255.1"
```
