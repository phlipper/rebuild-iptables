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
