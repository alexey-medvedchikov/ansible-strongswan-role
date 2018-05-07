# StrongSwan Ansible role

## Example configuration

`strongswan_cacerts` is for CA certificates:

```plain
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

`strongswan_certs` is for end entity certificates:

```plain
strongswan_certs:
  some.server.tld.pem: |-
    -----BEGIN CERTIFICATE-----
    ...
    -----END CERTIFICATE-----
  my.peer.tld.pem: |-
    -----BEGIN CERTIFICATE-----
    ...
    -----END CERTIFICATE-----
```

`strongswan_private` is for private keys:

```plain
strongswan_private:
  some.server.tld-key.pem: |-
    -----BEGIN RSA PRIVATE KEY-----
    ...
    -----END RSA PRIVATE KEY-----
```

List connections in ipsec.conf format:

```plain
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
