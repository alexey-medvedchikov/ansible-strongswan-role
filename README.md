# StrongSwan Ansible role

## Example configuration

To set `config setup` section use:

```yaml
strongswan_config: |-
  charondebug="cfg 2"
```

`strongswan_cacerts` is for CA certificates:

```yaml
strongswan_cacerts:
  ca.pem: |-
    -----BEGIN CERTIFICATE-----
    ...
    -----END CERTIFICATE-----
  intermediate.pem: |-
    -----BEGIN CERTIFICATE-----
    ...
    -----END CERTIFICATE-----
```

Also all types of file-based credentials available:

```yaml
strongswan_aacerts: {}
strongswan_acerts: {}
strongswan_cacerts: {}
strongswan_certs: {}
strongswan_crls: {}
strongswan_ocspcerts: {}
strongswan_private: {}
strongswan_reqs: {}
```

List connections in ipsec.conf format:

```yaml
strongswan_connections:
  '%default': |-
    ikelifetime=60m
    keylife=20m
    rekeymargin=3m
    keyingtries=%forever
    dpdaction=restart
    dpddelay=5s
    dpdtimeout=15s
    inactivity=0
    mobike=no

  'vpn-1': |-
    keyexchange=ikev2
    esp=aes256gcm128-aes256gmac
    left=%any
    leftcert=some.server.tld.pem
    leftid=@some.server.tld
    leftsubnet=0.0.0.0/0
    leftfirewall=yes
    right=10.10.10.10
    rightid=@my.peer.tld
    rightsubnet=0.0.0.0/0
    auto=start
```

Specify secrets:

```plain
strongswan_secrets:
  - ': RSA some.server.tld-key.pem'
```

## Authors

* Alexey Medvedchikov <alexey.medvedchikov@gmail.com>
