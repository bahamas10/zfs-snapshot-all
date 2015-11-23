ZFS Snapshot All
================

Recursively snapshot all zpools

Examples
--------

Snapshot all zpools with the prefix "foo"

    # ./zfs-snapshot-all foo
    zfs snapshot -r goliath@foo_1448256528
    zfs snapshot -r zones@foo_1448256528

Snapshot all zpools with the prefix "bar" without actually executing
any snapshot commands (dry-run)

    # ./zfs-snapshot-all -n bar
    zfs snapshot -r goliath@bar_1448256538 # dry-run: no action taken
    zfs snapshot -r zones@bar_1448256538 # dry-run: no action taken

Snapshot the pools given as arguments, "goliath", "zones", and "fake"
with the prefix "foo"

    # ./zfs-snapshot-all foo goliath zones fake
    zfs snapshot -r goliath@foo_1448256549
    zfs snapshot -r zones@foo_1448256549
    zfs snapshot -r fake@foo_1448256549
    cannot open 'fake': dataset does not exist
    # echo $?
    1

This script can be best used with cron for automated snapshots

    1 0 * * * /opt/custom/bin/zfs-snapshot-all automated_daily   >> /var/log/autosnap.log 2>&1
    2 0 * * 0 /opt/custom/bin/zfs-snapshot-all automated_weekly  >> /var/log/autosnap.log 2>&1
    3 0 1 * * /opt/custom/bin/zfs-snapshot-all automated_monthly >> /var/log/autosnap.log 2>&1
    4 0 1 1 * /opt/custom/bin/zfs-snapshot-all automated_yearly  >> /var/log/autosnap.log 2>&1

And then [zfs-prune-snapshots](https://github.com/bahamas10/zfs-prune-snapshots)
can be used to cleanup snapshots as they get too old... for example

    11 0 * * * /opt/custom/bin/zfs-prune-snapshots -p automated_daily_   7d   >> /var/log/autosnap.log 2>&1
    12 0 * * 0 /opt/custom/bin/zfs-prune-snapshots -p automated_weekly_  4w   >> /var/log/autosnap.log 2>&1
    13 0 1 * * /opt/custom/bin/zfs-prune-snapshots -p automated_monthly_ 12M  >> /var/log/autosnap.log 2>&1
    14 0 1 1 * /opt/custom/bin/zfs-prune-snapshots -p automated_yearly   10y  >> /var/log/autosnap.log 2>&1

Usage
-----

    usage: zfs-snapshot-all [-hnv] <name> [[pool1] pool2 ...]

    recursively snapshot all zpools

    examples
        # zfs-snapshot-all foo
        snapshot all zpools with the prefix foo

        # zfs-snapshot-all bar pool1 pool2
        snapshot zpools pool1 and pool2 with the prefix bar

    options
        -h             print this message and exit
        -n             dry-run, don't actually create snapshots

License
-------

MIT License
