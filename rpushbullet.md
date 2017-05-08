## RPushbullet

- get devices' IDs

  ```
  library(RPushbullet)
  devices <- pbGetDevices()$devices
  ```

- Just the active devices

  ```
  active_devices <- dplyr::filter(pbGetDevices()$devices, active)
  ```

- push a note

  ```
  pbPost("note", "title", "This is the body of the message.\nSecond line here.")
  ```
