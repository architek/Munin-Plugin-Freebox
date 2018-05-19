# NAME

freebox - Plugin for monitoring Freebox parameters.

# APPLICABLE SYSTEMS

Any computer that has access to a Freebox v6. Perl module [WWW::FBX](https://metacpan.org/pod/WWW::FBX)
is required for this plugin to function and can be installed from CPAN.

# INSTALLATION

    apt install munin-node
    apt install munin #only if you intend to run munin on the same host

    cpan install WWW::FBX
    git clone https://github.com/architek/Munin-Plugin-Freebox.git

Munin drops privileges with seteuid POSIX call. It inherits from default @INC. If you installed WWW::FBX using local::lib, adapt the use lib line at the start

# CONFIGURATION

## Link naming

Recommended way to limit connections to the freebox is by naming the plugin link as freebox\_multi. Adapt @multi array to select what to plot.

    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_multi

Otherwise, create links of what you want to plot. In that case, a new connection will be opened for every plot. This will increase CPU usage on both side, to a point where you might receive "Interal error" messages from the freebox.

    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_bandwidth
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_freeplug
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_temp
    sudo ln -s "$(pwd)/Munin-Plugin-Freebox/freebox_" /etc/munin/plugins/freebox_switch1

## Freebox authentication token

Just run auto configure. This will request app\\\_token and track\\\_id from the Freebox itself.

    sudo munin-run --debug freebox_multi autoconf

Add a freebox section in /etc/munin/plugin-conf.d/munin-node with values provided

    [freebox_*]
    user foo
    env.app_token value-of-the-token
    env.track_id value-of-the-track_id

## Self test

Check everything is working with:

    munin-run --debug freebox_multi

If not using multi mode:

    munin-run --debug freebox_bandwidth
    munin-run --debug freebox_freeplug
    munin-run --debug freebox_temp
    munin-run --debug freebox_switch1

# SCREENS

![Download and Upload graphs](https://user-images.githubusercontent.com/490053/34131111-96d4d4e8-e44a-11e7-9b32-64b261be0913.png)

*Download and Upload graphs from bandwidth category*

![Forward Error Corrections](https://user-images.githubusercontent.com/490053/34131136-ad98f9a2-e44a-11e7-87f2-df1916ec41af.png)

*Forward Error Corrections zoomed graph*

# LICENSE

GPLv2

# HISTORY

- 2014-07-19 Initial version.
- 2016-05-11 Modified.
