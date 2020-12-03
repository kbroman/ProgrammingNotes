## Docker

- For Ubuntu, want to install `docker-ce` ("Community edition") rather
  than `docker.io` (a now-out-of-date version)

  The instructions are [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/).

  Ended up doing:

  ```
  sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
  sudo apt-get install docker-ce docker-ce-cli containerd.io
  ```

- To install docker for minecraft, I changed to the directory
  containing the Dockerfile` in the miner package installation, and then
  followed the instructions in the [miner
  book](https://ropenscilabs.github.io/miner_book/installation-and-configuration.html#docker).

  ```
  cd ~/Rlibs/miner/Dockerfile .
  sudo docker build -t minecraft .
  ```

- To view the IP address of a docker container, type:

  ```
  ip addr show
  ```

  Look for lines following "docker"
