## sort

Command-line sort utility in unix


- `-h` = "human readable numbers", for example to sort directories by size:

  ```
  du -hd1 | sort -h
  ```

- `-t` = by time/date stamp

  ```
  ls -l | sort -t
  ```

- `-r` = reverse order

  ```
  ls -l | sort -rt
  ```

- `-k` = sort using a different column

  ```
  df -h | sort -hk2
  ```
