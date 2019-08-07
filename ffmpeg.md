## ffmpeg

- Extract part of a movie

  ```
  ffmpeg -ss 01:03:18 -i originalfile.m4v -t 00:00:04.35 -vcodec copy -acodec copy newfile.m4v
  ```

- Convert m4v to gif

  ```
  ffmpeg -i wake_up_unikitty.m4v -pix_fmt rgb8 -r 10 -y -s 720x360 wake_up_unikitty.gif
  ```
