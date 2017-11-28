# NAME

freebox - Plugin for monitoring Freebox parameters.

# APPLICABLE SYSTEMS

Any computer that has access to a Freebox v6. Perl module [WWW::FBX](https://metacpan.org/pod/WWW::FBX)
is required for this plugin to function and can be installed from CPAN.

# INSTALLATION

    apt install munin-node
    apt install munin #only if you intend to run munin on the same host

    cd $HOME && git clone https://github.com/architek/Munin-Plugin-Freebox.git

If you want to run the script as another user (recommended), make sure to have WWW::FBX in \*system-wide\* @INC or adapt the "use lib" line in the script if you use local::lib (recommended). System-wide INC is required as munin only changed EUID, RUID when changing user.
To have munin use an other user, create a freebox section in /etc/munin/plugin-conf.d/munin-node
    \[freebox\_\*\]
    user lke

# CONFIGURATION

Create links of what you want to plot

    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_bandwidth
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_freeplug
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_temp
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_switch1

Or use a multi graph call (the script will only be called once). By default are plotted: bandwidth, freeplug status, temperature, snr, fec, attn.

    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_

Now auto configure. This will request app\\\_token and track\\\_id from the Freebox itself.

    sudo munin-run --debug freebox_bandwidth autoconf

Add or complete the freebox section in /etc/munin/plugin-conf.d/munin-node with values provided

    [freebox_*]
    env.app_token value-of-the-token
    env.track_id value-of-the-track_id

Check everything is working with

    munin-run --debug freebox_bandwidth
    munin-run --debug freebox_freeplug
    munin-run --debug freebox_temp
    munin-run --debug freebox_switch1

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
