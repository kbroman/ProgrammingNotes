## ffmpeg

- Extract part of a movie

  ```
  ffmpeg -ss 01:03:18 -i originalfile.m4v -t 00:00:04.35 -vcodec copy -acodec copy newfile.m4v
  ```
