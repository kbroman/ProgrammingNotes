## bash

- loop to kill a sequence of PIDs
  (see [tldp howto](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-7.html))

  ```
  for i in `seq 18556 18570`
  do
      kill $i
  done
  ```
