
- [grimrock.net Scripting Reference](http://www.grimrock.net/modding/scripting-reference/) ([Local copy](./Legend-of-Grimrock-2/Scripting-Reference.md))
- [Item List](./Legend-of-Grimrock-2/Item-List.md)

# Console commands quick reference

```lua
party.party:heal()
party.party:getChampion(4):addSkillPoints(1) -- Gives one skill point to the bottom right champion.
party.party:getChampion(2):addSkillPoints(-1) -- Removes one skill point from the top right champion.
party.party:getChampion(1):modifyBaseStat("strength",  1)
party.party:getChampion(1):modifyBaseStat("dexterity", 1)
party.party:getChampion(1):modifyBaseStat("vitality",  1)
party.party:getChampion(1):modifyBaseStat("willpower", 1)
getMouseItem():setStackSize(100) -- Changes the count of the item held in the hand to 100.
getMouseItem():setStackable(true) -- Sets if the item held in the mouse is stackable
getMouseItem():setWeight(1) -- Set weight of item held in mouse
print( getMouseItem().go.name ) -- Print the name of the item that's held by the mouse.
spawn( getMouseItem().go.name ) -- Spawn the item that's held by the mouse.
party:setPosition(party.x+1, party.y+1, party.facing, party.elevation, party.level) -- Teleports party one space south and one space east.
```

```lua
party.party:getChampion(1)  // Top Left champion
party.party:getChampion(2)  // Top Right champion
party.party:getChampion(3)  // Bottom Left champion
party.party:getChampion(4)  // Bottom Right champion
```

```lua
-- Increase all base stats of all champions.
for i = 1,4 do for attr in ipairs({"strength", "dexterity", "vitality", "willpower"}) do party.party:getChampion(i):modifyBaseStat(attr, 1000) end end

-- Add skill points to all champions.
for i = 1,4 do party.party:getChampion(i):addSkillPoints(200) end
```

- Shortcut functions

The following code loads shortcut functions.

`--` and following characters are comments and don't need to be typed into the Grimrock console.

Once a function is created by typing the `function` line below, it will be available until the game is closed.

```lua

-- SSS = Set Stack Size
function sss(count) getMouseItem():setStackSize(count) end

-- Sets the count of the stack held in the mouse to 100
sss(100)

----------

function setStackable(isStackable) getMouseItem():setStackable(isStackable) end

-- Set the currently held item as stackable.
-- This could be dangerous for certain items.
-- Not recommended for notes/books/containers
setStackable(true)

----------

-- Clone what is held in the cursor.
-- This does not clone all properties. Cloning a note will produce a blank note, for example.
-- CMI = Clone Mouse Item
function cmi() spawn( getMouseItem().go.name ) end

cm()

----------

-- Teleport north/south, east/west, up/down, or any combination relative to the players current location.
function tp(x,y) party:setPosition(party.x + x, party.y + y, party.facing, party.elevation, party.level) end

-- Teleport north 1 space
tp(0,-1)

-- Teleport south 1 space
tp(0,1)

-- Teleport east  1 space
tp(1,0)

-- Teleport west  1 space
tp(-1,0)

-- Teleports east and south 1 space
tp(1,1)

----------

-- Teleport north/south, east/west, up/down, or any combination relative to the players current location.
function tpe(x,y,e) party:setPosition(party.x + x, party.y + y, party.facing, party.elevation + e, party.level) end

-- Teleport up   1 space
tpe(0,0,1)

-- Teleport down 1 space
tpe(0,0,-1)

```

- party:setPosition X and Y coordinates reference.

```
     y-1
      N
x-1 W + E x+1
      S
     y+1

Elevation +1 up, -1 down
```

- Note, as long as you have unspent skill points, your champion portraits will show "level up". If you add more skill points than you can spend, this message will be visible forever.

## Hunger

```lua
-- @param (number) $amount
-- party.party:getChampion( $ChampionIndex ):consumeFood( $amount )
party.party:getChampion(1):consumeFood(100)
```

## Gain Experience

```lua
-- party.party:getChampion( $ChampionIndex ):gainExp( $xp )

party:getChampion(1):gainExp(1000)
```

## Modify a champion stat

```lua
party.party:getChampion(1):modifyBaseStat("strength",  1)
party.party:getChampion(1):modifyBaseStat("dexterity", 1)
party.party:getChampion(1):modifyBaseStat("vitality",  1)
party.party:getChampion(1):modifyBaseStat("willpower", 1)
```

## Create an item on the floor in front of you

Make sure the space in front of you is empty.

```lua
spawn "wooden_box"
```

## Get the name of an item held in the mouse

You can then use this name to `spawn` an item.

```lua
print( getMouseItem().go.name )
```
