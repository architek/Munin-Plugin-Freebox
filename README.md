# NAME

freebox - Plugin for monitoring Freebox parameters.

# APPLICABLE SYSTEMS

Any computer that has access to a Freebox v6. Perl module [WWW::FBX](https://metacpan.org/pod/WWW::FBX)
is required for this plugin to function and can be installed from CPAN.

# INSTALLATION

    apt install munin-node
    apt install munin #only if you intend to run munin on the same host

Keep in mind that WWW::FBX should be reachable from root user (either through local::lib or system install). Munin drops privileges with seteuid POSIX call.

    cpan install WWW::FBX
    git clone https://github.com/architek/Munin-Plugin-Freebox.git

# CONFIGURATION

Recommended way is to limit connections to the freebox: Use a multi graph call. Adapt @multi array to select what to plot.

    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_multi

Otherwise, create links of what you want to plot. The drawback is that in that case, a new connection will be opened for every plot with added CPU usage.

    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_bandwidth
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_freeplug
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_temp
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_switch1

Now auto configure. This will request app\\\_token and track\\\_id from the Freebox itself.

    sudo munin-run --debug freebox_multi autoconf

Add a freebox section in /etc/munin/plugin-conf.d/munin-node with values provided

    [freebox_*]
    user foo
    env.app_token value-of-the-token
    env.track_id value-of-the-track_id

Check everything is working with:

    munin-run --debug freebox_multi

If not using multi mode:

    munin-run --debug freebox_bandwidth
    munin-run --debug freebox_freeplug
    munin-run --debug freebox_temp
    munin-run --debug freebox_switch1

# SCREENS

[![image.png](https://s8.postimg.org/g9lr05j5x/image.png)](https://postimg.org/image/phdzguq81/)

*Download and Upload graphs from bandwidth category*

[![image.png](https://s8.postimg.org/g9lr06tgl/image.png)](https://postimg.org/image/yp67xl7kx/)

*Forward Error Corrections zoomed graph*

# USAGE

This is a wildcard plugin which can be used to monitor several different
families of Freebox parameters. Run it with `suggest` command line argument
to see all the possible operation modes and create a symlink called
`freebox_mode` to this plugin from the Munin plugins directory, e.g.
`freebox_temp`.

# AUTHORS

Copyright 2014 Vadim Zeitlin <vz-cpan@zeitlins.org>

# LICENSE

GPLv2

# HISTORY

- 2014-07-19 Initial version.
- 2016-05-11 Modified.
