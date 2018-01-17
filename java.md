## Java

For the R packages ReporteRs (also rJava, xlsx, and WriteXLS) on a Mac, need to get java installed in the right way.
The following instructions seemed to work:

- <https://github.com/snowflakedb/dplyr-snowflakedb/wiki/Configuring-R-rJava-RJDBC-on-Mac-OS-X>

One change: for Java 8 development kit, I went to the following:

- <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>

Key steps:

- Install java 6
- Install java 8
- Run `sudo R CMD javareconf`
-
