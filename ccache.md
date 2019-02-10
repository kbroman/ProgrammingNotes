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

- For R, create a `~/.R/Makevars` file with something like the following:

  ```
  CC=ccache gcc
  CXX=ccache g++
  CFLAGS=-fpic -g -O2 -fstack-protector-strong -D_FORTIFY_SOURCE=2
  CXXFLAGS=-fpic -g -O2 -fstack-protector-strong -D_FORTIFY_SOURCE=2
  ```
