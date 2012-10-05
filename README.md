# rebuild-iptables

## Description

Construct an iptables rules file from fragments.

Constructs an iptables rules file from the prefix, standard, and suffix files in the iptables configuration area, adding any additional modules specified in the command line, and prints the resulting iptables rules to standard output (suitable for saving into /var/lib/iptables or some other appropriate location on the system).


## Requirements

### Supported Platforms

The following platforms are supported by this cookbook, meaning that the recipes run on these platforms without error:

* Ubuntu
* Debian
* CentOS
* Red Hat
* Fedora



## Usage

Write `iptables` rule fragments and place them in `/etc/iptables.d`. Running this script will assemble them in order and reset the firewall rules. 

## Example

For example, we have three rule-file:

`/etc/iptables.d/vagrant`

    # Vagrant boxes forwarding rules for public static ip

    *filter
    # Vagrand boxes forwarding ports
    -A FORWARD -p tcp -d 192.168.5.10 --dport 80 -j ACCEPT
    -A FORWARD -p tcp -d 192.168.5.10 --dport 22 -j ACCEPT

    *nat
    # Nat all traffic to vagrant boxes
    -A PREROUTING -d 192.168.25.2 -p tcp -j DNAT --to-destination 192.168.5.10
    -A POSTROUTING -j MASQUERADE
    COMMIT

`/etc/iptables.d/all_icmp`

    # ICMP 
    -A FWR -p icmp -j ACCEP

`/etc/iptables.d/all_estabilished`

    # Any established connection is money
    -A FWR -m state --state RELATED,ESTABLISHED -j ACCEPT

They are produce `/etc/iptables/general`

    *filter
    :INPUT ACCEPT [0,0]
    :FORWARD ACCEPT [0,0]
    :OUTPUT ACCEPT [0,0]
    :FWR -
    # Any established connection is money
    -A FWR -m state --state RELATED,ESTABLISHED -j ACCEPT
    # ICMP 
    -A FWR -p icmp -j ACCEPT
    # Vagrant boxes forwarding rules for public static ip

    # Vagrand boxes forwarding ports
    -A FORWARD -p tcp -d 192.168.5.10 --dport 80 -j ACCEPT
    -A FORWARD -p tcp -d 192.168.5.10 --dport 22 -j ACCEPT

    COMMIT
    *nat
    :PREROUTING ACCEPT [0,0]
    :POSTROUTING ACCEPT [0,0]
    :OUTPUT ACCEPT [0,0]
    # Nat all traffic to vagrant boxes
    -A PREROUTING -d 192.168.25.2 -p tcp -j DNAT --to-destination 192.168.5.10
    -A POSTROUTING -j MASQUERADE

    COMMIT


## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Added some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request


## License

**rebuild-iptables**

* Freely distributable and licensed under the [MIT license](http://phlipper.mit-license.org/2011-2012/license.html).
* Copyright (c) 2011-2012 Phil Cohen (github@phlippers.net) [![endorse](http://api.coderwall.com/phlipper/endorsecount.png)](http://coderwall.com/phlipper)
* http://phlippers.net/
