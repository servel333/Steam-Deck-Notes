
- [grimrock.net Scripting Reference](http://www.grimrock.net/modding/scripting-reference/) ([Local copy](./Legend-of-Grimrock-2/Scripting-Reference.md))

# Console commands quick reference

```lua
party.party:heal()
party.party:getChampion(4):addSkillPoints(1) -- Gives one skill point to the bottom right champion.
party.party:getChampion(2):addSkillPoints(-1) -- Removes one skill point from the top right champion.
getMouseItem():setStackSize(100) -- Changes the count of the item held in the hand to 100.
print( getMouseItem().go.name ) -- Print the name of the item that's held by the mouse.
spawn( getMouseItem().go.name ) -- Spawn the item that's held by the mouse.
party:setPosition(party.x+1, party.y+1, party.facing, party.elevation, party.level) -- Teleports party one space south and one space east.
```

```
party.party:getChampion(1)  // Top Left champion
party.party:getChampion(2)  // Top Right champion
party.party:getChampion(3)  // Bottom Left champion
party.party:getChampion(4)  // Bottom Right champion
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
