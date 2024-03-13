# Backing up DVDs

- download and install makemkv; see [this
  page](https://forum.makemkv.com/forum/viewtopic.php?f=3&t=224)

- install handbrake via apt

- also install libdvd-pkg via apt

- Use makemkv to rip DVD to a .mkv file

- Use handbrake to compress the .mkv file to m4v format

- To see title in the file:

  ```
  ffprobe -loglevel quiet -show_format input.m4v | grep title
  ```

- To change title in the file:

  ```
  ffmpeg -i input.m4v -codec copy -metadata title="New title" output.m4v
  ```

- To convert a .mov file to .mp4

  ```
  ffmpeg -i input.mov -vcodec h264 -acodec mp2 output.mp4
  ```
