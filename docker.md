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

- My slides about docker:
  - [without notes](https://kbroman.org/AdvData/26_containers.pdf)
  - [with notes](https://kbroman.org/AdvData/26_containers_notes.pdf)
  - [video of the lecture](https://us-lti.bbcollab.com/recording/0fc7d7a1d7ac472084798e61c43e4a63)

- For r-devel with R/qtl, create a Dockerfile with:

  ```
  FROM rocker/r-devel
  RUN R -e "install.packages('qtl')"
  ```

  and then do `sudo docker build -t rdevel-qtl .`

  That will create the image you want. Then run a container and open
  bash using:

  ```shell
  sudo docker run -it rdevel-qtl bash
  ```

  To install a package from github, use the
  [remotes](https://remotes.r-lib.org) package.

  Also note: with rocker/r-devel, you start R using `RD`.

- View images

  ```
  sudo docker images
  sudo docker image ls
  ```

- View running containers

  ```
  sudo docker container ls -a
  ```

- Start a container in interactive mode

  ```
  sudo docker start -i [container_name]
  ```

- Run a container from an image, interactively in a bash shell

  ```
  sudo docker run -it ubuntu bash
  ```

- Remove a running container

  ```
  sudo docker rm [container_name]
  ```
