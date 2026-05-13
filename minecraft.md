## minecraft commands

```
/defaultgamemode creative
```

```
/gamemode creative [user]
```

### movement

- w/a/s/d  - move forward/left/back/right
- space - jump / move up
- t - talk/chat
- left control - sprint
- left shift - sneak (and go down, if flying)
- `/` - open command
- attack/destroy - left button
- pick block - middle button
- use item/place block - right button
- q - drop selected item
- e - open inventory
- f - swap item with off hand

### movement if flying
- double-space - start or stop flying
- space - go up
- left shift - go down

### camera view

- F5 - toggle different perspectives

### stairs and door styles

- the [style for stair blocks](https://minecraft.fandom.com/wiki/Stairs#Block_states)
  has first two bits for direction and third bit for upright vs upside
  down.

  - 0-3 - upright, east/west/south/north
  - 4-7 - upside-down, east/west/south/north

  (ids are 53,67,108,109,114,128,134,135,136,156,163,164,180,203)

- the [style for door blocks](https://minecraft.fandom.com/wiki/Door#Block_states)
  has

  - first two bits for direction (east/south/west/north),
  - next bit for open/closed
  - next bit for lower/upper part of door

  (ids are 64,71,96,167,193-197,324,330,427-431)

  - seems like you need to set the top block before you set the bottom block

- pressure plates 70 for stone and 72 for wood
