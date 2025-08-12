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
  (It's also accessible only via adhara and not just using the VPN.)

  If connected on mylaptop via VPN, I get

  ```
  do_connect: Connection to research.drive.wisc.edu failed (Error NT_STATUS_UNSUCCESSFUL)
  ```

  Supposedly I can use `smph.vpn.wisc.edu` as the VPN address, but
  that didn't work for me either.

  It seems like the `NT_STATUS_UNSUCCESSFUL` is maybe a DNS problem.
  If I use the IP directly, `10.134.63.116`, I don't get that error.
  But instead I get `NT_STATUS_IO_TIMEOUT`. Tried also using `-U
  broman@ad.wisc.edu` but same error.

- To recursively move things including subdirectories:

  ```
  prompt OFF
  recurse ON
  mput *
  ```
