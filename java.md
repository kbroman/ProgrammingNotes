## Java

For the R packages
[ReporteRs](https://davidgohel.github.io/ReporteRs/) (also
[rJava](https://www.rforge.net/rJava/) and
[xlsx](https://github.com/dragua/xlsx)), need to get java
installed in the right way.

Here are Mac instructions:

- <https://github.com/snowflakedb/dplyr-snowflakedb/wiki/Configuring-R-rJava-RJDBC-on-Mac-OS-X>

On linux, I did:

```shell
sudo apt update
sudo apt install default-jre default-jdk
```

And then in my `~/.bashrc` file, I included

```shell
export JAVA_HOME="/usr/lib/jvm/default-java"
```

- <https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>

I also needed to run

```shell
sudo R CMD javareconf
```
