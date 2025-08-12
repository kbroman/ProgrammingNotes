## Research Drive (for UW-Madison)

- See instructions at https://kb.wisc.edu/researchdata/95148

- Need to use the VPN

- connect to a BCG computer

- Use `smbclient`

  ```
  smbclient -U broman@wisc.edu //research.drive.wisc.edu/payseur

  cd peicheng/read_counts_for_Karl
  ls
  get README_Backcross_Counting
  ```

- To download multiple files in `smbclient`, use the following:

  ```
  prompt OFF
  mget *.txt
  ```

- Can use `lcd` to change local directory.

- `exit` to exit

- My personal drive is at `//restricted.drive.wisc.edu/broman`

  Need to connect to GlobalProtect VPN using `smph.vpn.wisc.edu`
  (using login `broman` not `broman_1`).

  Needed to add `144.92.20.19` as DNS server in network settings
  (under IPv4). Found that server from <https://kb.wisc.edu/8958>.

- Was also able to connect using the Files app on my linux laptop.
  Connect to `smb://restricted.drive.wisc.edu/broman` and use
  broman@wisc.edu and password.

- To recursively move things including subdirectories:

  ```
  prompt OFF
  recurse ON
  mput *
  ```

- Can also mount drive on linus using `gio`:

  ```
  gio mount smb://restricted.drive.wisc.edu/broman
  gio mount --list
  ```

  It'll mount to `/var/run/user/$UID/gvfs/smb-share:server\=reserarch.drive.wisc.edu,share=broman`

  Unmount with

  ```
  gio mount -u smb://restricted.drive.wisc.edu/broman
  ```
