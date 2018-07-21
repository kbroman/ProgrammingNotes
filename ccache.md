# ccache

- Installation:

  ```shell
  sudo apt install ccache
  sudo /usr/sbin/update-ccache-symlinks
  export PATH="/usr/lib/ccache/:$PATH"
  ```

- Configuration: in `~/.ccache/ccache.conf`

  ```
  max_size = 10.0G
  hash_dir = false
  ```

- To view stats

  ```shell
  ccache -s
  ```

- To clear cache

  ```shell
  ccache --clear
  ```
