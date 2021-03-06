---
copyright:
  years: 2014, 2018
lastupdated: "2018-01-26"
---
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuring Riak networking

When you install Riak on an {{site.data.keyword.Bluemix}} engineered server, Riak is bound to the [private network IP address ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.softlayer.com/about/datacenters/rack-architecture){: new_window}. Binding Riak minimizes the security risks of having an open, accessible Riak instance exposed publicly upon deployment. At any time, the IP address that is bound to Riak can be changed. **Note:** Riak should not be exposed openly to public interfaces without other security measures in place to limit external access to the instance (for example, firewalls and iptables). 
{:shortdesc}

Complete the following steps to configure Riak networking to bind to a new interface.

## Binding Riak to a new interface

1. Go to the `riak_core` section of the `/etc/riak/app.config` file in the installation.
2. Update the `http{}` attribute in the `riak_core` section to reflect the new IP address to which Riak is bound.<br/>`{http, [ {"127.0.0.1", 8098 } ] },`
3. Locate the `/etc/vm.args` file in the installation.
4. Edit the `-name` attribute within the `/etc/vm.args` file to reflect the new IP address:<br/>`-name riak@127.0.0.1`
5. Restart Riak to complete the binding changes.

## Next Steps

The changes made to the bind impact all previous binds to any interfaces associated with the Riak instance. After restart, the bound IP address is updated and functioning properly. If you restart the Riak instance and it does not result in a successful bind, contact [Support](/docs/get-support/getstarttssup.html).
