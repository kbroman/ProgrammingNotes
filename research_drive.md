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
