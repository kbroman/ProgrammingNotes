## RPushbullet

- get devices' IDs

  ```
  devices <- pbGetDevices()$devices
  ```

- push a note

  ```
  pbPost("note", "title", "This is the body of the message.\nSecond line here.")
  ```
