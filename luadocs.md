# Function
* [Sleep](#Sleep)
* [LogToConsole](#LogToConsole)
* [SendPacket](#SendPacket)
* [SendPacketRaw](#SendPacketRaw)
* [FindPath](#FindPath)
* [GetTile](#GetTile)
* [GetTiles](#GetTiles) 

# Function Examples

Format:
`return_type Function(arguments)`

`return_type` = Type of value returned by function. Void functions will not return a value.

`Function` = Function name

`arguments` = Arguments of function. If the argument is formatted as `[, type argument_name]`, the argument is optional. If there is an "OR" in an argument, that means it can be multiple types.

## Sleep

`void Sleep(int length)`

Sleep for X milliseconds

Example:
```lua
Sleep(1000) -- 1000 Ms > 1 Second
```

## LogToConsole

`void LogToConsole(string text)`

Display Text in the Growtopia Chat System

Example:
```lua
LogToConsole("Hello World!") -- Displays "Hello World" in the Growtopia System Chat
```

## SendPacket

`void SendPacket(int type, string text)`

Send a text packet to the server

Example:
```lua
SendPacket(2, "action|input\ntext|Hello World!") -- Sends the message "Hello World!"
```

## SendPacketRaw

`void SendPacketRaw(bool client, TankPacket packet, [, int flags])`

Send [TankPacket](#TankPacket) to server/client. Flags is optional, default is 1.

Example:
```lua
-- Places an item with the id at (x, y)
local function place(id, x, y)
    pkt = {}
    pkt.type = 3
    pkt.value = id
    pkt.px = math.floor(GetLocal().posX / 32 + x)
    pkt.py = math.floor(GetLocal().posY / 32 + y)
    pkt.x = GetLocal().posX
    pkt.y = GetLocal().posY
    SendPacketRaw(false, pkt)
end
```

## FindPath

`bool FindPath(int x, int y [, int delay])`

Pathfinds (Finds a path and follows it) to the given coordinates. The function will return True if a path is found, False if a path is not found.

Example:
```lua
FindPath(10, 10) -- Pathfinds to (10, 10)
```

## GetTile

`Tile GetTile(int tile_x, int tile_y)`

Returns Tile struct of tile (x, y)

Example:
```lua
local tile = GetTile(10, 10) -- Returns tile struct of tile at (10, 10)
print(tile.fg) -- Prints foreground item id of tile
```

## GetTiles

`Tile[] GetTiles()`

Returns list of all Tile structs in current world. 

Example:
```lua
-- Finds coordinates (x, y) of tile by id in current world.
local function findTile(id)
	for _, tile in pairs(GetTiles()) do
		if tile.id == id then
			return tile.x, tile.y
		end
	end
end
```

