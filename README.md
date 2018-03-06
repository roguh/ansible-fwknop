fwknop
=========

Secure ports on your server from unauthorized access using fwknop, an improved port knocking utility.

> The main application of [fwknop] is to conceal services such as SSH with an additional layer of security in order to make the exploitation of vulnerabilities (both 0-day and unpatched code) much more difficult. In addition, services that are concealed in this fashion naturally cannot be scanned for with Nmap or Shodan. 

Requirements
------------

Make sure your firewall blocks access to any ports
you wish to hide. See `iptables-example` for sample iptables commands.

You need an fwknop client to reveal hidden ports and to setup the
fwknop key.
Install the `fwknop` package on Debian and Ubuntu,
or use one of the GUI clients

- [fwknop2 (Android app)](http://incomsystems.biz/linux/fwknop2/)
- [fwknop-gui](https://incomsystems.biz/fwknop-gui/),
- [jfwknop](https://github.com/fjoncourt/jfwknop).


Role Variables
--------------

| Variable | Description |
|--------------------|------------------------------------------------|
| `fwknop_pcap_intf` | Network interface fwknop listens to. Default `eth0`. |
| `fwknop_access_stanzas` | A list of access stanzas. Default: see `default_access_stanza` |

| Access Stanza Variable | Description
|------------------------|------------------------------------------------|
| `source` | Comma separated list of IP addresses or networks from which SPA packets are accepted, or `ANY`. Default `ANY`.
| `open_ports` | Comma separated list of protocol/port pairs to open. Default `tcp/22`.
| `key` | Symmetric key.
| `hmac_key` | Symmetric HMAC key.
| `key_base64` | Symmetric key encoded in base64.
| `hmac_key_base64` | Symmetric HMAC key encoded in base64.
| `fw_access_timeout` | Length of time access to `open_ports` in seconds. Default: `10`.
| `encryption_mode` | Set this to `legacy` if the fwknop server version is less than 2.5.
| `restrict_ports` | Ports that should NOT be allowed regardless of the validity of the incoming SPA packet.
| `destination` | Default: `ANY`.

Make sure to define at least `source` and `key` or `key_base64`.

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - role: roguh.fwknop
           fwknop_main_key_base64: YOUR_FWKNOP_KEY
           fwknop_main_hmac_key_base64: YOUR_FWKNOP_HMAC_KEY
```       

License
-------

MIT

More Information
------------------

[Read about fwknop at cipherdyne.org/fwknop](http://www.cipherdyne.org/fwknop/docs/).
