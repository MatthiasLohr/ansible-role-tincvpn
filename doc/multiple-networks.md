# Multiple tinc VPN networks

It's possible to set up multiple tinc networks in parallel by using the role multiple times:

```yaml
- hosts: group1
  roles:
    - role: steuf.tincvpn
      vars:
        tincvpn_network: "net1"
        tincvpn_subnet: "192.168.255.0/24"

- hosts: group2
  roles:
    - role: steuf.tincvpn
      vars:
        tincvpn_network: "net2"
        tincvpn_subnet: "192.168.42.0/24"
        tincvpn_port: 10655
```

You can specify node's VPN ip addresses in the inventory for each network:
```ini
[all]
node1 tincvpn_net1_ip=192.168.255.1 tincvpn_net2_ip=192.168.42.1
node2 tincvpn_net1_ip=192.168.255.2
node3                                incvpn_net2_ip=192.168.42.3

[group1]
node1
node2

[group2]
node1
node3
```
