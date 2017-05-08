## [RPushbullet](https://github.com/eddelbuettel/RPushbullet)

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

### In [R/broman](https://github.com/kbroman/broman)

- Send errors to Pushbullet

  ```
  broman::errors2pushbullet()
  ```

- Stop sending errors to Pushbullet

  ```
  broman::stop_sending_errors()
  ```

- Send a note to Pushbullet

  ```
  broman::note("title")
  ```

- Send a super-short "R is done" message

  ```
  broman::done()
  ```

- `recipients` in these functions are the names defined in
  `~/.rpushbullet.json`.
