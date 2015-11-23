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
