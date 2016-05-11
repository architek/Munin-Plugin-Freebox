# NAME

freebox - Plugin for monitoring Freebox parameters.

# APPLICABLE SYSTEMS

Any computer that has access to a Freebox v6. Perl module [WWW::FBX](https://metacpan.org/pod/WWW::FBX)
is required for this plugin to function and can be installed from CPAN.

# CONFIGURATION

    cp freebox_ /etc/munin/plugins

    cd /etc/munin/plugins

    ln -s freebox_ freebox_bandwidth
    ln -s freebox_ freebox_freeplug
    ln -s freebox_ freebox_temp

To configure, run autoconf
 ./freebox\_ autoconf

And add a freebox section in /etc/munin/plugin-conf.d/munin-node as follow

    [freebox_*]
    env.app_token value-of-the-token
    env.track_id value-of-the-track_id

Check everything is working with
 munin-run --debug freebox\_bandwidth
 munin-run --debug freebox\_freeplug
 munin-run --debug freebox\_temp

# USAGE

This is a wildcard plugin which can be used to monitor several different
families of Freebox parameters. Run it with `suggest` command line argument
to see all the possible operation modes and create a symlink called
`freebox_mode` to this plugin from the Munin plugins directory, e.g.
`freebox_temp`.

# AUTHORS

Copyright 2014 Vadim Zeitlin <vz-cpan@zeitlins.org>

Modified by Laurent Kislaire

# LICENSE

GPLv2

# HISTORY

- 2014-07-19 Initial version.
- 2016-05-11 Modified.

# MAGIC MARKERS

    #%# family=manual
    #%# capabilities=autoconf suggest
