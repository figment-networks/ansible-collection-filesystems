# Format Role

See defaults for all documented options and configuration.

Example playbooks at the root of the collection.

## Mounting a device at one or more paths

By default a device is mounted at a single path using `format_mount_point`
(and, optionally, `format_mount_options`). To mount the same device at more
than one path, use `format_mount_points` instead:

```yaml
format_mount_points:
  mount_points:
    - /srv/bsc
    - /var/lib/private/bsc
  mount_options: noatime,nodiratime  # optional, defaults to "defaults"
```

`format_mount_point`/`format_mount_options` and `format_mount_points` are
mutually exclusive — set one or the other, not both.

Whichever form is used, the role enforces that `/etc/fstab` only contains
entries for the paths currently declared for `format_device`. If a device's
mount point configuration changes (or a path is dropped from
`format_mount_points`), any fstab entry left over from a previous run for
that same device is removed automatically. This lookup and cleanup is
scoped strictly to `format_device`, so entries for unrelated devices (for
example, the root filesystem) are never touched.
