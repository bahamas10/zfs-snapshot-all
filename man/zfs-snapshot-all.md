ZFS-SNAPSHOT-ALL 1 "NOV 2018" "User Commands"
=============================================

NAME
----

`zfs-snapshot-all` - Recursively snapshot all zpools

SYNOPSIS
--------

`zfs-snapshot-all [OPTIONS] <name> [[pool1] pool2 ...]`

DESCRIPTION
-----------

Recursively snapshot all or a subset of zpools

OPTIONS
-------

`-h`
  print this message and exit

`-n`
  dry-run, don't actually create snapshots

`-x`
  don't automatically append the date in epoch to the snapshot name

`-V`
  print the version number and exit

EXAMPLES
--------

`zfs-snapshot-all foo`
  snapshot all zpools with the prefix foo

`zfs-snapshot-all bar pool1 pool2`
  snapshot zpools pool1 and pool2 with the prefix bar

`zfs-snapshot-all -x baz pool3`
  snapshot zpool pool3 with the *exact* snapshot name 'baz'

BUGS
----

https://github.com/bahamas10/zfs-snapshot-all

AUTHOR
------

`Dave Eddy <bahamas10> <dave@daveeddy.com> (https://www.daveeddy.com)`

SEE ALSO
--------

zpool(1M), zfs(1M)

LICENSE
-------

MIT License
