## rsync

"remote sync" for synchronizing local and remote files
Looking at <http://do.co/2BpIpZe>

- `-r` = recursive

- `-a` = archive (recursively and preserves symbolic links,
  modification times, group, owner, and permissions)

- `-v` = verbose

- `-n` = dry run

- `-z` = reduce network transfer by adding compression

- `-P` = `--progress` (progress bar) + `--partial` (allows you to
  resume interrupted transfers)

- `--delete` = delete stuff from destination if removed from source

To sync contents of `dir1` with `dir2`:

```
rsync -a dir1/ dir2
```

Trial run:

```
rsync -avn dir1/ dir2
```

Syncing remotely, and pushing the full directory:

```
rsync -a dir1 username@host:dir2
```
