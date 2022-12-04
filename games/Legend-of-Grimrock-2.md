
# Scripting Reference

<!--
Contents

AmmoItemComponent
AnimationComponent
BeaconFurnaceControllerComponent
BlastComponent
BlindedMonsterComponent
BombItemComponent
BossFightComponent
BrainComponent
BurningMonsterComponent
ButtonComponent
CameraComponent
CameraShakeComponent
CastSpellComponent
Champion
ChestComponent
ClickableComponent
CloudSpellComponent
Component
Config
Console
ContainerItemComponent
ControllerComponent
CounterComponent
CrabBrainComponent
CraftPotionComponent
CrowControllerComponent
CrowernAttackComponent
CrystalComponent
CrystalShardItemComponent
DamageFlags
DiggingToolComponent
DoorComponent
Dungeon
DynamicObstacleComponent
EarthquakeComponent
Editor
EntangledMonsterComponent
EquipmentItemComponent
ExitComponent
EyctopusBrainComponent
FireElementalBrainComponent
FirearmAttackComponent
FloorTriggerComponent
FogParamsComponent
FogParticlesComponent
ForceFieldComponent
FrozenMonsterComponent
GameMode
GameObject
GoromorgBrainComponent
GoromorgShieldComponent
GraphicsContext
GravityComponent
HealthComponent
HeightmapComponent
HerderBigBrainComponent
HerderSmallBrainComponent
IceGuardianBrainComponent
IceLizardBrainComponent
IceShardsComponent
ItemActionComponent
ItemComponent
ItemConstrainBoxComponent
ItemSlot
LadderComponent
LensFlareComponent
LeverComponent
LightComponent
LindwormBrainComponent
LindwormChargeComponent
LindwormFlyComponent
LockComponent
MagmaGolemBrainComponent
Map
MapGraphicsComponent
MapMarkerComponent
MaterialEx
MeleeAttackComponent
MeleeBrainComponent
MersenneTwister
MimicCameraAnimationComponent
ModelComponent
MonsterActionComponent
MonsterAttackComponent
MonsterChangeAltitudeComponent
MonsterChargeComponent
MonsterComponent
MonsterDropItemComponent
MonsterGroupComponent
MonsterJumpComponent
MonsterKnockbackComponent
MonsterLightCullerComponent
MonsterMoveAttackComponent
MonsterMoveComponent
MonsterOperateDeviceComponent
MonsterPickUpItemComponent
MonsterStealWeaponComponent
MonsterTurnComponent
MonsterWarpComponent
MosquitoSwarmBrainComponent
NullComponent
ObstacleComponent
OccluderComponent
OgreBrainComponent
ParticleComponent
PartyComponent
PitComponent
PlatformComponent
PoisonCloudAttackComponent
PoisonedMonsterComponent
PortalComponent
ProjectileColliderComponent
ProjectileComponent
ProjectileImpactComponent
PullChainComponent
PushableBlockComponent
PushableBlockFloorComponent
RangedAttackComponent
RangedBrainComponent
RatlingBossBrainComponent
ReloadFirearmComponent
RopeToolComponent
RunePanelComponent
ScriptComponent
ScriptControllerComponent
ScrollItemComponent
SecretComponent
SkeletonArcherBrainComponent
SkeletonCommanderBrainComponent
SkyComponent
SleepingMonsterComponent
SlimeBrainComponent
SmallFishControllerComponent
SocketComponent
SoundComponent
SpawnerComponent
SpellScrollItemComponent
StairsComponent
StatisticsComponent
StonePhilosopherControllerComponent
StunnedMonsterComponent
SurfaceComponent
SwarmBrainComponent
TeleporterComponent
TentacleBrainComponent
TentacleHideComponent
ThornWallComponent
ThrowAttackComponent
TileDamagerComponent
Time
TimerComponent
TinyCritterControllerComponent
ToadBrainComponent
TorchHolderControllerComponent
TorchItemComponent
TricksterBrainComponent
TurtleBrainComponent
TwigrootBrainComponent
UggardianBrainComponent
UggardianFlamesComponent
UsableItemComponent
ViperRootBrainComponent
WallTextComponent
WallTriggerComponent
WargBrainComponent
WaterSurfaceComponent
WaterSurfaceMeshComponent
WizardBrainComponent
XeloroidBrainComponent
ZarchtonBrainComponent
-->

Welcome!

You are reading the Lua scripting reference manual for Legend of Grimrock 2.
The focus of this document is on completeness rather than brevity.
Refer to the tutorials for more detailed examples on how to use the material described here.

The Lua functions and methods described here can be accessed from a script entity and typed on the console.

In addition the following standard Lua functions can be used:

- tonumber
- tostring
- type
- pairs
- ipairs
- and all functions in table
- math and string modules.

See the Lua reference manual for more details about their usage.

## Entities and Components

Entities, game objects (or just `go`) are the objects spawned in the dungeon either by placing them in the dungeon using the Dungeon Editor or spawning them dynamically from a script.

For example, instances of buttons, pressure plates, teleporters and the party are all entities. Each entity has an id, a string which identifies the entity uniquely. You can refer to an entity by simply typing it’s id. For example, the following script prints the world coordinates of the entity with the id `party` to the console:

- `print(party:getWorldPosition())`

Entities themselves do not have much useful functionality. Instead, interesting objects are made by adding components to the entities. For example, you would build an object with a 3D model that emits a continuous sound by adding a Model and a Sound component to an entity. A component is always created and owned by a single entity and components cannot exists without an entity. Each component has a class, e.g. Door and Model are classes, and a name which uniquely identifies the components inside its entity. By default the name of a component is the class name in lower case but you can pick any name when defining assets. Usually one entity can have only one component of a kind (for example, single Door component per entity) but some components do not have this restriction. For example, an entity can have any number of Model, Light, Particle and Sound components. In this case, each component must be explicitly and uniquely named (for example, `model1`, `model2`).

All entities have the following properties that can be accessed with the dot operator:

- `name`: returns the name of the entity
- `id`: returns the unique identifier of the entity
- `x`: returns the x-coordinate of the entity on the map
- `y`: returns the y-coordinate of the entity on the map
- `elevation`: returns the elevation of the entity on the map (`0 = ground level`)
- `facing`: returns the facing of the entity (`0=north`, `1=east`, `2=south`, `3=west`)
- `level`: returns the dungeon level index of the entity
- `map`: returns the Map object representing the dungeon level where the entity is
- `xyz`: returns the component named `xyz` (or nil if no such component exists)

For example, `torch1.x` would return the x-coordinate of the entity named `torch1`, and `torch1.light` would returns the component named `light`.

All components have the following properties that can be accessed with the dot operator:

- `go`: returns the entity that owns the component

For example, `item.go.model` would return the component named `model` attached to the item component.

You can also refer to the script entity itself from its own script code using the implicit `self` variable. This can be handy if you need to refer to it’s coordinates. For example the following script prints the x- and y-coordinates of the script entity to the console:

- `print(self.x, self.y)`

Some special objects have no direct representation of them in the dungeon. For example, a Champion is an object that is contained inside the Party entity. You have no direct access to these objects but various functions return references to them. For example, the following script retrieves the first champion in the party and changes his name:

- `party.party:getChampion(1):setName("Jakob")`

## Global Functions

### `print(…)`

Prints all arguments to the console.

### `iff(cond, a, b)`

Returns a if cond is true, otherwise returns b.

### `vec(x, y, z, w)`

Returns a new vector. All components are optional and default to zero.

### `getForward(direction)`

Converts direction, a number between 0 and 3 corresponding to a compass direction, to delta-x and delta-y values.

### `getDirection(dx, dy)`

### `toLocal(ox, oy, facing, x, y)`

### `delayedCall(receiver, delay, msg)`

### `spawn(object, level, x, y, facing, elevation, [id])`

Spawns a new object at given position on a dungeon level where x and y specify the x- and y-coordinates on the map and level is a level index. facing must be a number between 0 and 3 and it indicates the following directions: `0 = north`, `1 = east`, `2 = south`, `3 = west`. id parameter is optional. If given it must be an unique id in the context of the dungeon. If not given an unique id is automatically generated.

### `findEntity(id)`

Returns an entity with given name or nil if no such entity exists.

### `hudPrint(text)`

Prints a line of text to the text area at the bottom of the screen.

### `setMouseItem(item)`

Sets the given item as mouse item, or destroys the mouse item if item is nil.

### `getMouseItem()`

Returns the `mouse item`, the item attached to the mouse pointer. If there is no mouse item, nil is returned.

### `playSound(sound)`

Plays a sound effect. sound must be a name of a built-in or custom sound effect.

### `playSoundAt(sound, level, x, y)`

Plays a sound effect at given position. sound must be a name of a built-in or custom sound effect.

### `rollDamage(power)`

Returns a random amount of damage for an attack with given power.

### `damageTile(level, x, y, direction, elevation, flags, damageType, power)`

Damages all creatures including the party in a given tile. direction specifies the direction of the attack for projectiles or melee attacks (`0=north`, `1=east`, `2=south`, `3=west`).

- `damageType` must be one of the following: `physical`, `fire`, `poison`, `cold`, `shock`.

Damage is rolled individually for all creatures using the power as base value.

See also DamageFlags.

### `shootProjectile(projectile, level, x, y, direction, speed, gravity, velocityUp, offsetX, offsetY, offsetZ, attackPower, ignoreEntity, fragile, championOrdinal)`

Shoots a projectile item.

The parameters are:

- `projectile`: the name of the item to shoot.
- `level,x,y`: the initial position of the projectile in a level.
- `direction`: the shooting direction (0=north, 1=east, 2=south, 3=west).
- `speed`: the speed of the projectile (metres/second). Typical values around 10.
- `gravity`: the gravity force in y-direction. Typical values around 0.
- `velocityUp`: the initial velocity in y-direction. Typically set to 0.
- `offsetX`,offsetY,offsetZ: 3D offset in world space from the center of cell.
- `attackPower`: attack power of the projectile.
- `ignoreEntity`: the entity to be ignored for collisions (or nil if the entity should not ignore any collisions).
- `fragile`: a boolean flag, if set the projectile is destroyed on impact.
- `championOrdinal`: a champion ordinal number, used for dealing experience points. This parameter is optional.

## Asset Definitions

The following functions can be used in dungeon’s init.lua script to define new assets.

### `defineAnimationEvent(desc)`

Defines a new animation event.

`desc` is a table with the following fields:

- `animation`: the name of animation file to attach animation event to. The filename must end with `.fbx`
- `event`: the animation event string, e.g. `footstep` or `attack`.
- `frame`: (optional) a frame number in the animation to attach the event to (one frame equals 1/30th of a second).
- `normalizedTime`: (optional) normalized time of the event in range 0-1 to be used instead of frame (0 = start of animation, 1 = end of animation).

### `defineObject(desc)`

Defines a new entity type or replaces an existing definition.

`desc` is a table with the following fields:

- `name`: the name of the object to define or replace.
- `baseObject`: (optional) the name of the base object definition to clone.
- `components`: an array of components to add or override (see below).
- `placement`: placement of the object in the square: `floor`, `ceiling`, `wall` or `pillar`.
- `replacesWall`: (optional) a boolean, if true the object removes an existing wall object when spawned.
- `replacesFloor`: (optional) a boolean, if true the object removes an existing floor object when spawned.
- `replacesCeiling`: (optional) a boolean, if true the object removes an existing ceiling object when spawned.
- `editorIcon`: index of the icon in Dungeon Editor.
- `automapTile`: (optional) automap tile type: `ground`, `grassy_ground`, `water`, `wall`, `rocky_wall`, `trees` or `chasm`.
- `automapIcon`: (optional) icon index in automap icon sheet.

The components field should contain a list of components to be added or replaced in the base object class.
Each component has a class and a name. The name of a component is by default its class in lower case.

Each component have the following fields:

- `class`: the class name of the component without the `Component` part. E.g. `Model`.
- `name`: (optional) the name of the component. Convention is to use lower case names.
- `enabled`: (optional) the initial enabled state of the component (default is true).
- `xyz`: (optional) sets the xyz property of the component by calling `setXyz()` method of the component. Any setter that receives a single parameters can be called using this mechanism.
- `onXyz`: (optional) adds the xyz hook to the component.

See component classes for details on properties and hooks supported by various components.

### `defineSound(desc)`

Defines a new sound or replaces an existing sound definition. The samples used need to be 16bit 44100Hz .wav-files.

`desc` is a table with the following fields:

- `name`: the name of the sound to define or replace.
- `filename`: the filename of the sample in wave format. The filename must be a valid asset reference ending with `.wav`. Optionally the filename may be a table containing multiple filenames for random sound variations.
- `loop`: a boolean which turns on and off looping.
- `volume`: a number between 0 and 1 which controls the amplitude of the sound.
- `minDistance`: the minimum distance in squares for sound falloff. The sound plays at max volume if it is closer than min distance to the listener.
- `maxDistance`: the maximum distance in squares for sound falloff. The sound is not audible after max distance.

### `defineParticleSystem(desc)`

Defines a new particle system or replaces an existing particle system definition.

`desc` is a table with the following fields:

- `name`: the name of the particle system to define or replace.
- `emitters`: a table of emitter descriptors. See below.

An emitter descriptor is a table which contains the parameters for a particle emitter.

The following parameters are supported:

- `emitterShape`: type of the emitter, either `BoxShape` (default) or `MeshShape`.
- `emissionRate`: number of particles to emit per second.
- `emissionTime`: duration of emission in seconds. If set to zero, emission time is infinite.
- `maxParticles`: maximum number of active particles. Sensible values are between 100 and 1000.
- `spawnBurst`: if enabled maximum number of particles are emitted in a single burst when the particle system is started.
- `boxMin`: a 3D vector defining the minimum extents for particle emission.
- `boxMax`: a 3D vector defining the maximum extents for particle emission.
- `sprayAngle`: a table whose first and second elements set the minimum and maximum spraying angle in degrees.
- `velocity`: a table whose first and second elements set the minimum and maximum velocity in units per second.
- `size`: a table whose first and second elements set the minimum and maximum size for for emitted particles.
- `lifeTime`: a table whose first and second elements set the minimum and maximum lifetime for emitted particles.
- `texture`: a valid texture asset reference. The texture may contain multiple frames laid out on a grid.
- `frameSize`: (optional) pixel size of a frame in the particle animation sequence. Typically 32 or 64.
- `frameCount`: (optional) total number of frames in the particle animation sequence.
- `frameRate`: (optional) frame rate of the particle animation sequence.
- `color0`: a table containing R,G,B values in range 0-1 for initial particle color.
- `color1,color2,color3`: (optional) particle color sequence. These parameters have no effect if colorAnimation is not enabled.
- `colorAnimation`: a boolean which enables particle color animation.
- `opacity`: particle opacity value between 0 and 1.
- `fadeIn`: particle’s fade in time in seconds.
- `fadeOut`: particle’s fade out time in seconds.
- `gravity`: a 3D gravity vector.
- `airResistance`: air resistance parameter. Sensible values are between 0 and 10.
- `rotationSpeed`: rotation speed of particles in degrees.
- `randomInitialRotation`: a boolean flag, if enabled particles’ initial rotation angle is randomized.
- `blendMode`: blending mode for particle rendering. Must be either `Additive` or `Translucent`.
- `objectSpace`: a boolean flag, if enabled particles are emitted to object space rather than world space.
- `clampToGroundPlane`: a boolean flag, if enabled particles collide against the ground.
- `depthBias`: depth bias value in world space units.

### `defineRace(desc)`

Defines a new race or replaces an existing race definition.

`desc` is a table with the following fields:

- `name`: the name of the race to define or replace.
- `uiName`: the name of the race displayed to the user.
- `inventoryBackground`: filename of the background texture in character sheet.

A champion automatically gains the trait with the same name as his race.

### `defineCharClass(desc)`

Defines a new character class or replaces an existing class definition.

`desc` is a table with the following fields:

- `name`: the name of the race to define or replace.
- `uiName`: the name of the race displayed to the user.
- `traits`: (optional) list of extra traits provided by the character class.
- `skillPoints`: (optional) number of skill points received at first level (default is 2).

A champion automatically gains the trait with the same name as his character class.

### `defineSkill(desc)`

Defines a new skill or replaces an existing skill definition.

`desc` is a table with the following fields:

- `name`: the name of the skill to define or replace.
- `uiName`: the name of the skill displayed to the user.
- `priority`: sorting priority for UI. Built-in skills have priorities 10,20,30,…
- `icon`: icon index in the skill texture atlas.
- `iconAtlas`: (optional) filename of the icon atlas. Icons are 75×75 and the width and height of the atlas must be multiple of icon size.
- `description`: textual description of the skill.
- `gameEffect`: (optional) textual description of the game effect provided by the skill.
- `traits`: (optional) a table of new traits gained when progressing in the skill. For example, ``{ [3] = `pack_mule` }``.
- `onRecomputeStats(champion, skillLevel)`: (optional) a hook for modifying champion’s attributes based on skill level. champion:addStatModifier() can be called from inside the hook.
- `onComputeAccuracy(champion, weapon, attack, attackType, skillLevel)`: (optional) a hook for modifying accuracy of an attack. The function should return an accuracy modifier.
- `onComputeCritChance(champion, weapon, attack, attackType, skillLevel)`: (optional) a hook for modifying critical hit chance of an attack. The function should return a critical hit modifier.

### `defineTrait(desc)`

Traits work almost exactly like skills except they are on/off rather than having a level.

See `defineSkill()` for a list of supported fields.

The following additional fields are supported for traits:

- `charGen`: (optional) a boolean, if set the trait can be chosen at character creation.
- `requiredRace`: (optional) the name of the race for racial traits.
- `hidden`: (optional) a boolean, if set the trait is not shown in Traits tab.

### `defineMaterial(desc)`

Defines a new material or replaces an existing material definition.

`desc` is a table with the following fields:

- `name`: the name of the material to define or replace.
- `shader`: (optional) name of the built-in shader.
- `diffuseMap`: (optional) the filename of the diffuse texture. The filename must be valid asset reference ending with `.tga`. If no texture is specified a built-in white texture is used.
- `specularMap`: (optional) the filename of the specular texture. The filename must be valid asset reference ending with `.tga`. If no texture is specified a built-in white texture is used.
- `normalMap`: (optional) the filename of the normal map. The filename must be valid asset reference ending with `.tga`. If no texture is specified normal mapping is turned off.
- `doubleSided`: (optional) a boolean specifying whether the surface using the material can be seen from both sides.
- `lighting`: (optional) a boolean which turns on and off dynamic lighting.
- `castShadow`: (optional) a boolean which turns on and off shadow casting.
- `ambientOcclusion`: (optional) a boolean which turns on and off ambient occlusion.
- `alphaTest`: (optional) a boolean which turns on and off alpha testing.
- `blendMode`: (optional) the alpha blending mode, must be one of the following: `Opaque`, `Translucent`, `Additive`, `Modulative`.
- `textureAddressMode`: (optional) texture addressing mode:`Wrap`, `Clamp`, `WrapU_ClampV_WrapW`, `ClampU_WrapV_WrapW`, `WrapU_ClampV_ClampW` or `ClampU_WrapV_ClampW`.
- `glossiness`: (optional) the glossiness parameter for specular lighting. Typical values range between 1 and 100.
- `depthBias`: (optional) depth bias value. It is recommended to set this always to zero.
- `onUpdate(material, time)`: (optional) hook to be called every frame. It can be used to animate materials.

### `defineSpell(desc)`

Defines a new spell or replaces an existing spell.

`desc` is a table with the following fields:

- `name`: the name of the spell to define.
- `uiName`: the name shown to the user (e.g. in spell scrolls).
- `skill`: the name of the skill used to cast the spell.
- `requirements`: the requirements for this spell, e.g. { `concentration`, 3 }.
- `gesture`: a numeric value encoding the spell gesture (see below).
- `manaCost`: number of mana points to spend when casting the spell.
- `icon`: index of the skill icon in Traits tab.
- `iconAtlas`: (optional) filename of the icon atlas. Icons are 75×75 and the width and height of the atlas must be multiple of icon size.
- `spellIcon`: index of the spell preview icon in rune panel.
- `spellIconAtlas`: (optional) filename of the spell icon atlas. Spell icons are 50×50 and the width and height of the atlas must be multiple of icon size.
- `description`: textual description of the spell.
- `onCast(champion, x, y, direction, elevation, skillLevel)`: built-in spell function name or a custom spell function.

Spell gestures are encoded into numeric values.
Each digit in the number corresponds to a rune.

The available runes are:

- 1 = Fire
- 2 = Life
- 3 = Air
- 4 = Spirituality
- 5 = Balance
- 6 = Physicality
- 7 = Earth
- 8 = Death
- 9 = Water

```
+-----------+
|  1  2  3  |
|  4  5  6  |
|  7  8  9  |
+-----------+
```

For example, `1236` would be the gesture of the Fireball spell.

### `defineRecipe(desc)`

Defines a new potion recipe or replases an existing recipe.

`desc` is a table with the following fields:

- `name`: the name of the potion recipe to define or replace.
- `level`: Alchemy skill level needed to craft the potion.
- `ingredients`: a number describing the ingredients.

Ingredients are encoded into numeric value.
Each digit in the number corresponds to an herb.

The available herbs are:

- 1 = Blooddrop Cap
- 2 = Etherweed
- 3 = Mudwort
- 4 = Falconskyre
- 5 = Blackmoss
- 6 = Crystal Flower

For example, `115` would translate to a recipe with two Blooddrop Caps and one Blackmoss.

### `defineTile(desc)`

Defines a new tile for Dungeon Editor or replases an existing definition.

`desc` is a table with the following fields:

- `name`: the name of the tile to define or replace.
- `editorIcon`: index of the icon in Dungeon Editor tile atlas.
- `color`: (optional) color of the editor icon, e.g. {255,255,255,255} is solid white.
- `randomFloorFacing`: (optional) a boolean, when true facing of spawned floor objects will be randomized.
- `solid`: (optional) a boolean, if true the square is solid wall.
- `diggable`: (optional) a boolean, if true the square can be digged.
- `underwater`: (optional) a boolean, if true the square is under water.
- `heightmapMaterial`: (optional) material name for heightmap building.
- `heightmapMaterialPriority`: (optional) priority for heightmap material blending. Higher priority materials blends over low priority materials.
- `builder`: (optional) type of geometry builder, `dungeon` or `mine`.
- `floor`: (optional) a table of floor object names and their relative probabilities. See below.
- `wall`: (optional) a table of wall object names and their relative probabilities. See below.
- `pillar`: (optional) a table of pillar object names and their relative probabilities. See below.
- `centerPillar`: (optional) a table of pillar object names to be placed in the center of cells and their relative probabilities for mine builder. See below.
- `ceiling`: (optional) a table of ceiling object names and their relative probabilities. See below.
- `ceilingShaft`: (optional) the name of the object automatically spawned if there’s a pit above.
- `ceilingEdgeVariations`: (optional) a boolean, if set ceiling objects use 16 different variations for all possible configurations of adjacent tiles. A bitmask _XXXX will be appended to ceiling object name, where each bit is either 0 (adjancent tile is empty space) or 1 (adjacent tile is solid).
- `automapTile`: (optional) the name of the automap tile: `ground`, `grassy_ground`, `water`, `wall`, `rocky_wall`, `trees` or `chasm`
- `moveSound`: (optional) the name of sound played when the party walks on the tile.

The tables referred above contain lists of objects and their probabilities that are used to randomly pick up pieces for generating the levels.
At every odd table index there must be a valid object name.
At every even table index there must be a number that indicates the relative probability of the object.

For example, the following would generate a wall drain approximately every 50th generated wall:

```
wall = {
  "dungeon_wall_01", 50,
  "dungeon_wall_drain", 1,
}
```

## AmmoItemComponent (Component)

Makes an item ammo for missile or firearm attack. The ammo types must match in the Ammo component and the attack component.

- `AmmoItemComponent:getAmmoType()`	Get ammunition type which must match with weapon’s ammo type
- `AmmoItemComponent:getAttackPower()`	Get damage bonus to weapon’s base damage
- `AmmoItemComponent:setAmmoType(string)`	Set ammunition type which must match with weapon’s ammo type
- `AmmoItemComponent:setAttackPower(number)`	Set damage bonus to weapon’s base damage

## AnimationComponent (Component)

Adds animations to the 3D model attached to the same GameObject. The GameObject must have a Model component.

- `AnimationComponent:crossfade(name, length)`
- `AnimationComponent:getCurrentLevelOnly()`	Get whether animation component is updated only when party is on the same level
- `AnimationComponent:getLoop()`	Get looping for initial animation
- `AnimationComponent:getMaxUpdateDistance()`	Get max update distance in squares
- `AnimationComponent:getPlayOnInit()`	Get name of the initial animation to be played when the object is spawned
- `AnimationComponent:play(name)`
- `AnimationComponent:sample()`
- `AnimationComponent:setCurrentLevelOnly(boolean)`	Set whether animation component is updated only when party is on the same level
- `AnimationComponent:setLoop(boolean)`	Set looping for initial animation
- `AnimationComponent:setMaxUpdateDistance(number)`	Set max update distance in squares
- `AnimationComponent:setPlayOnInit(string)`	Set name of the initial animation to be played when the object is spawned
- `AnimationComponent:stop()`
- `AnimationComponent.onAnimationEvent(self, event)`

## BeaconFurnaceControllerComponent (Component)

Implements the behavior of altars in Elemental Shrines. The name of the class is weird because of historical reasons.

- `BeaconFurnaceControllerComponent:getElement()`
- `BeaconFurnaceControllerComponent:setElement(string)`

## BlastComponent (Component)

Spawns objects in 2 square radius area. Used to implement Magma Golem’s flame wave attack.

- `BlastComponent:getDelay()`
- `BlastComponent:getEffect()`
- `BlastComponent:setDelay(number)`
- `BlastComponent:setEffect(string)`

## BlindedMonsterComponent (Component)

## BombItemComponent (Component)

Makes a thrown item explode when it hits something.

- `BombItemComponent:getBombPower()`
- `BombItemComponent:getBombType()`
- `BombItemComponent:setBombPower(number)`
- `BombItemComponent:setBombType(string)`

## BossFightComponent (Component)

Implements boss fights. When activated, bossfight music starts and a progress bar is displayed at the top of the screen. The boss fight ends automatically when all monsters taking part in it are destroyed or it can be manually deactivated.

- `BossFightComponent:activate()`
- `BossFightComponent:addMonster(monster)`
- `BossFightComponent:deactivate()`
- `BossFightComponent:getAchievement()`
- `BossFightComponent:getAutoDeactivate()`
- `BossFightComponent:getBossName()`
- `BossFightComponent:getMusic()`
- `BossFightComponent:recomputeTotal()`
- `BossFightComponent:removeMonster(monster)`
- `BossFightComponent:setAchievement(string)`
- `BossFightComponent:setAutoDeactivate(boolean)`
- `BossFightComponent:setBossName(string)`
- `BossFightComponent:setMusic(string)`

## BrainComponent (Component)

Base-class for all monster brains. You can either use one of the built in brains (e.g. TurleBrain) or implement a custom onThink hook. When the monster is ready to perform a new action, the brain’s onThink hook is called. The brain should respond by calling monster component’s performAction() method with a valid action name. The brain class itself contains many higher level behaviors such as fleeing and pursuit which can be used in place of performAction() to delegate decision making. If the brain can not decide what to do, Brain:wait() should be called. This will put the monster’s brain to sleep for a short time (typically 0.1s) to prevent extensive CPU usage.

- `BrainComponent:alert()`
- `BrainComponent:carrying(string)`
- `BrainComponent:changeAltitude()`
- `BrainComponent:charge()`
- `BrainComponent:circleStrafeHesitate()`
- `BrainComponent:circleStrafeStall()`
- `BrainComponent:dropItem(string)`
- `BrainComponent:dropItemOn(string, string)`
- `BrainComponent:flee()`
- `BrainComponent:follow()`
- `BrainComponent:getAllAroundSight()`	Get whether the monster can see in any direction
- `BrainComponent:getMorale()`	Get morale rating in range 0-100 (0 = coward, 100 = fearless)
- `BrainComponent:getSeeInvisible()`	Get whether the monster can sense invisible things (such as invisible party members)
- `BrainComponent:getSight()`	Get maximum sight range in squares
- `BrainComponent:goTo(string)`
- `BrainComponent:here(string)`
- `BrainComponent:isSafeTile(x, y)`
- `BrainComponent:meleeAttack()`
- `BrainComponent:moveBackward()`
- `BrainComponent:moveForward()`
- `BrainComponent:moveTowardsParty()`
- `BrainComponent:openLockWith(string, string)`
- `BrainComponent:operate(string)`
- `BrainComponent:performAction(…)`
- `BrainComponent:pickUpItem(string, boolean)`
- `BrainComponent:pursuit()`
- `BrainComponent:rangedAttack()`
- `BrainComponent:seek(number)`
- `BrainComponent:setAllAroundSight(boolean)`	Set whether the monster can see in any direction
- `BrainComponent:setMorale(number)`	Set morale rating in range 0-100 (0 = coward, 100 = fearless)
- `BrainComponent:setSeeInvisible(boolean)`	Set whether the monster can sense invisible things (such as invisible party members)
- `BrainComponent:setSight(number)`	Set maximum sight range in squares
- `BrainComponent:startFleeing()`
- `BrainComponent:startGuarding()`
- `BrainComponent:stepTowards(string, number)`
- `BrainComponent:stopFleeing()`
- `BrainComponent:stopGuarding()`
- `BrainComponent:strafeLeft()`
- `BrainComponent:strafeRight()`
- `BrainComponent:turnAround()`
- `BrainComponent:turnAroundAttack()`
- `BrainComponent:turnAttack()`
- `BrainComponent:turnAttackLeft()`
- `BrainComponent:turnAttackRight()`
- `BrainComponent:turnLeft()`
- `BrainComponent:turnRight()`
- `BrainComponent:turnTowardsDirection()`
- `BrainComponent:turnTowardsParty()`
- `BrainComponent:turnTowardsTarget()`
- `BrainComponent:wait()`
- `BrainComponent:wander()`
- `BrainComponent:wanderIfPartyNotDetected()`
- `BrainComponent.onThink(self)`
- `BrainComponent.onBloodied(self)`

## BurningMonsterComponent (Component)

Implements the burning condition for monsters. A monster with the burning condition is dealt ongoing fire damage until the effect’s duration ends or the monster dies.

- `BurningMonsterComponent:getCausedByChampion()`
- `BurningMonsterComponent:setCausedByChampion(number)`

## ButtonComponent (Component)

Implements wall button mechanics for an object. Requires Clickable and Animation component. When the object is clicked, the button component plays a sound, tells the animation component to play `press` animation clip and triggers its onActivate hook and connectors.

- `ButtonComponent:getDisableSelf()`
- `ButtonComponent:getSound()`
- `ButtonComponent:setDisableSelf(boolean)`
- `ButtonComponent:setSound(string)`
- `ButtonComponent.onActivate(self)`

## CameraComponent (Component)

Custom camera component for rendering from arbitrary view point.

- `CameraComponent.onUpdate(self)`

## CameraShakeComponent (Component)

## CastSpellComponent (ItemActionComponent)

Implements cast spell actions for spell wands. When used, a spell stored in the wand is cast. Optionally the wand may have limited number of charges.

- `CastSpellComponent:deplete()`
- `CastSpellComponent:getCharges()`
- `CastSpellComponent:getEmptyGfxIndex()`
- `CastSpellComponent:getEmptyItem()`
- `CastSpellComponent:getFullGfxIndex()`
- `CastSpellComponent:getMaxCharges()`
- `CastSpellComponent:getPower()`
- `CastSpellComponent:getRequiredLevel()`
- `CastSpellComponent:getSkill()`
- `CastSpellComponent:getSpell()`
- `CastSpellComponent:recharge()`
- `CastSpellComponent:setCharges(number)`
- `CastSpellComponent:setEmptyGfxIndex(number)`
- `CastSpellComponent:setEmptyItem(string)`
- `CastSpellComponent:setFullGfxIndex(number)`
- `CastSpellComponent:setMaxCharges(number)`
- `CastSpellComponent:setPower(number)`
- `CastSpellComponent:setRequiredLevel(number)`
- `CastSpellComponent:setSkill(string)`
- `CastSpellComponent:setSpell(string)`

## Champion

Champion’s attributes, skills, traits, conditions and other statistics can be accessed through this class.

- `Champion:addSkillPoints(amount)`
- `Champion:addStatModifier(name, amount)`
- `Champion:addTrait(name)`
- `Champion:attack(number, boolean)`
- `Champion:castSpell(number)`
- `Champion:consumeFood(amount)`
- `Champion:damage(dmg, damageType)`
- `Champion:gainExp(xp)`
- `Champion:getArmorSetPiecesEquipped(name)`
- `Champion:getBaseStat(name)`
- `Champion:getClass()`
- `Champion:getConditionValue(name)`
- `Champion:getCurrentStat(name)`
- `Champion:getDualClass()`
- `Champion:getEnabled()`
- `Champion:getEnergy()`
- `Champion:getEvasion()`
- `Champion:getExp()`
- `Champion:getFood()`
- `Champion:getHealth()`
- `Champion:getItem(slot)`
- `Champion:getLevel()`
- `Champion:getLoad()`
- `Champion:getMaxEnergy()`
- `Champion:getMaxHealth()`
- `Champion:getMaxLoad()`
- `Champion:getName()`
- `Champion:getOrdinal()`
- `Champion:getOtherHandItem(slot)`
- `Champion:getProtection()`
- `Champion:getRace()`
- `Champion:getResistance(element)`
- `Champion:getSex()`
- `Champion:getSkillLevel(name)`
- `Champion:getSkillPoints()`
- `Champion:hasCondition(name)`
- `Champion:hasTrait(name)`
- `Champion:insertItem(slot, item)`
- `Champion:isAlive()`
- `Champion:isArmorSetEquipped(name)`
- `Champion:isBodyPartWounded(slot)`
- `Champion:isDualWielding()`
- `Champion:isReadyToAttack(number)`
- `Champion:levelUp()`
- `Champion:modifyBaseStat(name, value)`
- `Champion:modifyFood(amount)`
- `Champion:playDamageSound()`
- `Champion:playHealingIndicator()`
- `Champion:playSound(name)`
- `Champion:regainEnergy(amount)`
- `Champion:regainHealth(amount)`
- `Champion:removeCondition(name)`
- `Champion:removeItem(item)`
- `Champion:removeItemFromSlot(slot)`
- `Champion:removeTrait(name)`
- `Champion:setBaseStat(name, value)`
- `Champion:setClass(class)`
- `Champion:setCondition(name)`
- `Champion:setConditionValue(name, value)`
- `Champion:setEnabled(enabled)`
- `Champion:setEnergy(energy)`
- `Champion:setFood(food)`
- `Champion:setHealth(health)`
- `Champion:setName(name)`
- `Champion:setPortrait(filename)`
- `Champion:setRace(race)`
- `Champion:setSex(sex)`
- `Champion:setSkillPoints(points)`
- `Champion:showAttackResult(any, string)`
- `Champion:swapItems(slot1, slot2)`
- `Champion:swapWeaponSets()`
- `Champion:trainSkill(name, times)`
- `Champion:upgradeBaseStat(name, value)`

## ChestComponent (Component)

Implements the chest opening and closing animations. A chest be optionally locked and it could be mimic.

- `ChestComponent:getLocked()`
- `ChestComponent:getMimic()`
- `ChestComponent:setLocked(locked)`
- `ChestComponent:setMimic(boolean)`

## ClickableComponent (Component)

Defines the click box of an object. onClick hook is called when the player clicks on the object. A GameObject can have any number of Clickables.

- `ClickableComponent:getDebugDraw()`
- `ClickableComponent:getFrontFacing()`	Get whether the party needs to face the clickable to use it (default false)
- `ClickableComponent:getMaxDistance()`	Get maximum distance in squares (default 0)
- `ClickableComponent:getSize()`
- `ClickableComponent:setDebugDraw(boolean)`
- `ClickableComponent:setFrontFacing(boolean)`	Set whether the party needs to face the clickable to use it (default false)
- `ClickableComponent:setMaxDistance(number)`	Set maximum distance in squares (default 0)
- `ClickableComponent:setSize(size)`
- `ClickableComponent.onClick(self)`

## CloudSpellComponent (Component)

A CloudSpell deals ongoing damage to party, monsters and obtacles in the same square. The component is automatically destroyed when its duration runs out.

- `CloudSpellComponent:getAttackPower()`
- `CloudSpellComponent:getCastByChampion()`
- `CloudSpellComponent:getDamageInterval()`
- `CloudSpellComponent:getDamageType()`
- `CloudSpellComponent:getDuration()`
- `CloudSpellComponent:getSound()`
- `CloudSpellComponent:setAttackPower(number)`
- `CloudSpellComponent:setCastByChampion(number)`
- `CloudSpellComponent:setDamageInterval(number)`
- `CloudSpellComponent:setDamageType(string)`
- `CloudSpellComponent:setDuration(time)`
- `CloudSpellComponent:setSound(string)`

## Component

Base-class for all Components. A Component always belongs to one and only one GameObject. Components can be enabled and disabled. A disabled component usually acts as it would not exist in the game.

- `Component:addConnector(event, target, action)`
- `Component:disable()`
- `Component:enable()`
- `Component:getConnector(i)`
- `Component:getConnectorCount()`
- `Component:getOffset()`
- `Component:isEnabled()`
- `Component:removeConnector(event, target, action)`
- `Component:setOffset(offset)`
- `Component:setRotationAngles(x, y, z)`
- `Component.onInit(self)`

## Config

- `Config.getKeyBinding(action)`
- `Config.getRenderingQuality()`

## Console

- `Console.suppressWarnings(suppress)`
- `Console.warn(msg)`

## ContainerItemComponent (Component)

Makes an item a container for other items.

- `ContainerItemComponent:addItem(item)`
- `ContainerItemComponent:getCapacity()`
- `ContainerItemComponent:getContainerType()`
- `ContainerItemComponent:getItem(slot)`
- `ContainerItemComponent:getItemCount()`
- `ContainerItemComponent:insertItem(slot, item)`
- `ContainerItemComponent:removeItem(item)`
- `ContainerItemComponent:removeItemFromSlot(slot)`
- `ContainerItemComponent:setContainerType(string)`
- `ContainerItemComponent.onInsertItem(self, item, slot)`
- `ContainerItemComponent.onRemoveItem(self, item, slot)`

## ControllerComponent (Component)

Generic controller component which can be used to implement custom activate/deactivate/toggle, open/close, increment/decrement or start/stop semantics for an object. For example, if you add onActivate and onDeactivate hooks to the Controller, the controller can act as target for activate and deactivate events in the Dungeon Editor.

- `ControllerComponent:activate()`
- `ControllerComponent:close()`
- `ControllerComponent:deactivate()`
- `ControllerComponent:decrement()`
- `ControllerComponent:getInitialState()`
- `ControllerComponent:increment()`
- `ControllerComponent:open()`
- `ControllerComponent:pause()`
- `ControllerComponent:reset()`
- `ControllerComponent:setInitialState(string)`
- `ControllerComponent:start()`
- `ControllerComponent:stop()`
- `ControllerComponent:toggle()`
- `ControllerComponent.onInitialActivate(self)`
- `ControllerComponent.onInitialDeactivate(self)`
- `ControllerComponent.onInitialOpen(self)`
- `ControllerComponent.onInitialClose(self)`
- `ControllerComponent.onActivate(self)`
- `ControllerComponent.onDeactivate(self)`
- `ControllerComponent.onToggle(self)`
- `ControllerComponent.onOpen(self)`
- `ControllerComponent.onClose(self)`
- `ControllerComponent.onIncrement(self)`
- `ControllerComponent.onDecrement(self)`
- `ControllerComponent.onStart(self)`
- `ControllerComponent.onStop(self)`
- `ControllerComponent.onPause(self)`

## CounterComponent (Component)

Counters start with an initial value and count down when activated. When counter’s value reaches zero, it calls its onActivate hook and triggers onActivate connectors.

- `CounterComponent:decrement()`
- `CounterComponent:getValue()`
- `CounterComponent:increment()`
- `CounterComponent:reset()`
- `CounterComponent:setInitialValue(number)`
- `CounterComponent:setValue(value)`
- `CounterComponent.onActivate(self)`
- `CounterComponent.onDeactivate(self)`

## CrabBrainComponent (BrainComponent)

Implements AI for Cave Crabs.

## CraftPotionComponent (Component)

## CrowControllerComponent (Component)

## CrowernAttackComponent (Component)

## CrystalComponent (Component)

Implements the animation and behavior of healing crystals.

- `CrystalComponent:activate()`
- `CrystalComponent:deactivate()`
- `CrystalComponent:getCooldown()`
- `CrystalComponent:setCooldown(number)`

## CrystalShardItemComponent (Component)

## DamageFlags

- `DamageFlags.Impact = 1`
- `DamageFlags.OngoingDamage = 2`
- `DamageFlags.Champion1 = 4`
- `DamageFlags.Champion2 = 8`
- `DamageFlags.Champion3 = 16`
- `DamageFlags.Champion4 = 32`
- `DamageFlags.IgnoreImmunities = 64`
- `DamageFlags.HalveBackRowDamage = 128`
- `DamageFlags.CameraShake = 256`
- `DamageFlags.NoLingeringEffects = 512`
- `DamageFlags.DamageSourceIceShards = 1024`

## DiggingToolComponent (Component)

## DoorComponent (Component)

Door component blocks movement and projectiles from passing between two adjacent squares. Requires a Model component with a node named `gate`. The gate node is animated when the door is opened and closed. Doors can either open vertically (single doors) or horizontally (double doors).

- `DoorComponent:close()`
- `DoorComponent:getCloseAcceleration()`
- `DoorComponent:getCloseSound()`
- `DoorComponent:getCloseVelocity()`
- `DoorComponent:getDoorState()`
- `DoorComponent:getDoubleDoor()`
- `DoorComponent:getHitSound()`	Get sound to play when the door is hit
- `DoorComponent:getKillPillars()`
- `DoorComponent:getLockSound()`
- `DoorComponent:getMaxHeight()`
- `DoorComponent:getOpenSound()`
- `DoorComponent:getOpenVelocity()`
- `DoorComponent:getOpeningDirection()`
- `DoorComponent:getPullChain()`
- `DoorComponent:getPullchainObject()`	Get custom pullchain object
- `DoorComponent:getSecretDoor()`	Get secret doors are not visible on the map
- `DoorComponent:getSparse()`
- `DoorComponent:isClosed()`
- `DoorComponent:isClosing()`
- `DoorComponent:isOpen()`
- `DoorComponent:isOpening()`
- `DoorComponent:isPassable()`
- `DoorComponent:open()`
- `DoorComponent:setCloseAcceleration(number)`
- `DoorComponent:setCloseSound(string)`
- `DoorComponent:setCloseVelocity(number)`
- `DoorComponent:setDoorState(state)`
- `DoorComponent:setDoubleDoor(boolean)`
- `DoorComponent:setHitSound(string)`	Set sound to play when the door is hit
- `DoorComponent:setKillPillars(boolean)`
- `DoorComponent:setLockSound(string)`
- `DoorComponent:setMaxHeight(number)`
- `DoorComponent:setOpenSound(string)`
- `DoorComponent:setOpenVelocity(number)`
- `DoorComponent:setOpeningDirection(string)`
- `DoorComponent:setPullChain(enable)`
- `DoorComponent:setPullchainObject(string)`	Set custom pullchain object
- `DoorComponent:setSecretDoor(boolean)`	Set secret doors are not visible on the map
- `DoorComponent:setSparse(boolean)`
- `DoorComponent:toggle()`
- `DoorComponent.onOpen(self)`
- `DoorComponent.onClose(self)`
- `DoorComponent.onAttackedByChampion(self, champion, weapon, attack, slot)`

## Dungeon

- `Dungeon.getMap(i)`
- `Dungeon.getMaxLevels()`

## DynamicObstacleComponent (Component)

## EarthquakeComponent (Component)

## Editor

- `Editor.isRunning()`

## EntangledMonsterComponent (Component)

## EquipmentItemComponent (Component)

Implemented various modifiers to stats of an Champion when the item is equipped. The traits of an item define where the item can be equipped.

- `EquipmentItemComponent:getAccuracy()`	Get accuracy modifier
- `EquipmentItemComponent:getCooldownRate()`	Get cooldown rate modifier
- `EquipmentItemComponent:getCriticalChance()`	Get critical chance modifier
- `EquipmentItemComponent:getDamage()`
- `EquipmentItemComponent:getDexterity()`	Get dexterity modifier
- `EquipmentItemComponent:getEnergy()`	Get energy modifier
- `EquipmentItemComponent:getEnergyRegenerationRate()`	Get energy regeneration rate modifier
- `EquipmentItemComponent:getEvasion()`	Get evasion modifier
- `EquipmentItemComponent:getExpRate()`	Get experience rate modifier
- `EquipmentItemComponent:getFoodRate()`	Get food consumption rate modifier
- `EquipmentItemComponent:getHealth()`	Get health modifier
- `EquipmentItemComponent:getHealthRegenerationRate()`	Get health regeneration rate modifier
- `EquipmentItemComponent:getProtection()`	Get protection modifier
- `EquipmentItemComponent:getResistCold()`	Get cold resistance modifier
- `EquipmentItemComponent:getResistFire()`	Get fire resistance modifier
- `EquipmentItemComponent:getResistPoison()`	Get poison resistance modifier
- `EquipmentItemComponent:getResistShock()`	Get shock resistance modifier
- `EquipmentItemComponent:getSlot()`
- `EquipmentItemComponent:getStrength()`	Get strength modifier
- `EquipmentItemComponent:getVitality()`	Get vitality modifier
- `EquipmentItemComponent:getWillpower()`	Get willpower modifier
- `EquipmentItemComponent:setAccuracy(number)`	Set accuracy modifier
- `EquipmentItemComponent:setCooldownRate(number)`	Set cooldown rate modifier
- `EquipmentItemComponent:setCriticalChance(number)`	Set critical chance modifier
- `EquipmentItemComponent:setDamage(number)`
- `EquipmentItemComponent:setDexterity(number)`	Set dexterity modifier
- `EquipmentItemComponent:setEnergy(number)`	Set energy modifier
- `EquipmentItemComponent:setEnergyRegenerationRate(number)`	Set energy regeneration rate modifier
- `EquipmentItemComponent:setEvasion(number)`	Set evasion modifier
- `EquipmentItemComponent:setExpRate(number)`	Set experience rate modifier
- `EquipmentItemComponent:setFoodRate(number)`	Set food consumption rate modifier
- `EquipmentItemComponent:setHealth(number)`	Set health modifier
- `EquipmentItemComponent:setHealthRegenerationRate(number)`	Set health regeneration rate modifier
- `EquipmentItemComponent:setProtection(number)`	Set protection modifier
- `EquipmentItemComponent:setResistCold(number)`	Set cold resistance modifier
- `EquipmentItemComponent:setResistFire(number)`	Set fire resistance modifier
- `EquipmentItemComponent:setResistPoison(number)`	Set poison resistance modifier
- `EquipmentItemComponent:setResistShock(number)`	Set shock resistance modifier
- `EquipmentItemComponent:setSlot(number)`
- `EquipmentItemComponent:setStrength(number)`	Set strength modifier
- `EquipmentItemComponent:setVitality(number)`	Set vitality modifier
- `EquipmentItemComponent:setWillpower(number)`	Set willpower modifier
- `EquipmentItemComponent.onRecomputeStats(self, champion)`
- `EquipmentItemComponent.onComputeAccuracy(self, champion, weapon, attack, attackType)`
- `EquipmentItemComponent.onComputeCritChance(self, champion, weapon, attack, attackType)`

## ExitComponent (Component)

## EyctopusBrainComponent (BrainComponent)

Implements AI for Eyctopuses.

## FireElementalBrainComponent (BrainComponent)

Implements AI for Fire Elementals.

## FirearmAttackComponent (ItemActionComponent)

Implements firearm attacks. Firearm attacks need ammo.

- `FirearmAttackComponent:getAccuracy()`	Get optional accuracy bonus
- `FirearmAttackComponent:getAmmo()`	Get type of ammo needed to fire the weapon (optional)
- `FirearmAttackComponent:getAttackPower()`	Get attack power of the attack
- `FirearmAttackComponent:getAttackSound()`	Get name of the sound effect to play (default is `swipe`)
- `FirearmAttackComponent:getBaseDamageStat()`	Get base statistic used for computing damage modifier (default none)
- `FirearmAttackComponent:getClipSize()`	Get (optional) clip size for revolver like weapons
- `FirearmAttackComponent:getDamageType()`	Get damage type of the attack: `physical` (default), `cold`, `fire`, `poison` or `shock`
- `FirearmAttackComponent:getLoadedCount()`	Get (optional) how much ammo is currently loaded in the revolver
- `FirearmAttackComponent:getPierce()`	Get how many points of armor is bypassed by the attack
- `FirearmAttackComponent:getRange()`	Get range in squares
- `FirearmAttackComponent:getRequiredLevel()`
- `FirearmAttackComponent:getSkill()`
- `FirearmAttackComponent:setAccuracy(number)`	Set optional accuracy bonus
- `FirearmAttackComponent:setAmmo(string)`	Set type of ammo needed to fire the weapon (optional)
- `FirearmAttackComponent:setAttackPower(number)`	Set attack power of the attack
- `FirearmAttackComponent:setAttackSound(string)`	Set name of the sound effect to play (default is `swipe`)
- `FirearmAttackComponent:setBaseDamageStat(number)`	Set base statistic used for computing damage modifier (default none)
- `FirearmAttackComponent:setClipSize(number)`	Set (optional) clip size for revolver like weapons
- `FirearmAttackComponent:setDamageType(string)`	Set damage type of the attack: `physical` (default), `cold`, `fire`, `poison` or `shock`
- `FirearmAttackComponent:setLoadedCount(number)`	Set (optional) how much ammo is currently loaded in the revolver
- `FirearmAttackComponent:setPierce(number)`	Set how many points of armor is bypassed by the attack
- `FirearmAttackComponent:setRange(number)`	Set range in squares
- `FirearmAttackComponent:setRequiredLevel(number)`
- `FirearmAttackComponent:setSkill(string)`
- `FirearmAttackComponent.onBackfire(self, champion)`
- `FirearmAttackComponent.onPostAttack(self, champion, slot)`

## FloorTriggerComponent (Component)

A floor trigger reacts to objects placed into trigger’s square. A floor trigger can be in two states: activated and deactivated. When an object is placed on a deactivated trigger, it changes to activated state and fires its onActivate hooks and connectors. Similarly when an object is removed from the square of an activated trigger, the trigger changes into deactivated state and fires its onDeactivate hooks and connectors.

- `FloorTriggerComponent:getActivateSound()`
- `FloorTriggerComponent:getDeactivateSound()`
- `FloorTriggerComponent:getDisableSelf()`
- `FloorTriggerComponent:getPressurePlate()`	Get whether the floor trigger is part of an actual pressure plate device (camera is tilted down when standing on pressure plates, etc.)
- `FloorTriggerComponent:getTriggeredByDigging()`
- `FloorTriggerComponent:getTriggeredByEntityType()`
- `FloorTriggerComponent:getTriggeredByItem()`
- `FloorTriggerComponent:getTriggeredByMonster()`
- `FloorTriggerComponent:getTriggeredByParty()`
- `FloorTriggerComponent:getTriggeredByPushableBlock()`
- `FloorTriggerComponent:isActivated()`
- `FloorTriggerComponent:isDeactivated()`
- `FloorTriggerComponent:setActivateSound(string)`
- `FloorTriggerComponent:setDeactivateSound(string)`
- `FloorTriggerComponent:setDisableSelf(boolean)`
- `FloorTriggerComponent:setPressurePlate(boolean)`	Set whether the floor trigger is part of an actual pressure plate device (camera is tilted down when standing on pressure plates, etc.)
- `FloorTriggerComponent:setTriggeredByDigging(boolean)`
- `FloorTriggerComponent:setTriggeredByEntityType(string)`
- `FloorTriggerComponent:setTriggeredByItem(boolean)`
- `FloorTriggerComponent:setTriggeredByMonster(boolean)`
- `FloorTriggerComponent:setTriggeredByParty(boolean)`
- `FloorTriggerComponent:setTriggeredByPushableBlock(boolean)`
- `FloorTriggerComponent.onActivate(self)`
- `FloorTriggerComponent.onDeactivate(self)`
- `FloorTriggerComponent.onToggle(self)`

## FogParamsComponent (Component)

Overrides fog parameters for indoor scenes. This component is used to make the fog green in Herder’s Den level in the main campaign. Only works indoors! The Sky component defines fog parameters for outdoor scenes.

- `FogParamsComponent:getFogColor()`
- `FogParamsComponent:getFogMode()`
- `FogParamsComponent:getFogRange()`
- `FogParamsComponent:setFogColor(vec)`
- `FogParamsComponent:setFogMode(string)`
- `FogParamsComponent:setFogRange(table)`

## FogParticlesComponent (Component)

Adds particle fog effect to the scene. The effect quite heavy on performance so use it wisely.

- `FogParticlesComponent:getColor1()`
- `FogParticlesComponent:getColor2()`
- `FogParticlesComponent:getColor3()`
- `FogParticlesComponent:getOpacity()`
- `FogParticlesComponent:getParticleSize()`
- `FogParticlesComponent:getTexture()`
- `FogParticlesComponent:setColor1(vec)`
- `FogParticlesComponent:setColor2(vec)`
- `FogParticlesComponent:setColor3(vec)`
- `FogParticlesComponent:setOpacity(number)`
- `FogParticlesComponent:setParticleSize(number)`
- `FogParticlesComponent:setTexture(texture)`

## ForceFieldComponent (Component)

## FrozenMonsterComponent (Component)

## GameMode

- `GameMode.advanceTime(amount)`
- `GameMode.completeGame(filename)`
- `GameMode.fadeIn(color, length)`
- `GameMode.fadeOut(color, length)`
- `GameMode.getTimeOfDay()`
- `GameMode.playStream(name)`
- `GameMode.playVideo(filename)`
- `GameMode.setCamera(camera)`
- `GameMode.setMaxStatistic(stat, max)`
- `GameMode.setStatistic(stat)`
- `GameMode.setTimeOfDay(time)`
- `GameMode.showImage(filename)`

## GameObject

GameObject is a container for Components. A GameObject has a position and orientation in the world.

- `GameObject:createComponent(string)`
- `GameObject:destroy()`
- `GameObject:destroyDelayed()`
- `GameObject:getComponent(name)`
- `GameObject:getElevation()`
- `GameObject:getFullId()`
- `GameObject:getPosition()`
- `GameObject:getSubtileOffset()`
- `GameObject:getWorldForward()`
- `GameObject:getWorldPosition()`
- `GameObject:getWorldPositionY()`
- `GameObject:getWorldRotation()`
- `GameObject:playSound(name)`
- `GameObject:removeAllComponents()`
- `GameObject:removeComponent(component)`
- `GameObject:setPosition(x, y, facing, elevation, level)`
- `GameObject:setSubtileOffset(x, y)`
- `GameObject:setWorldPosition()`
- `GameObject:setWorldPositionY(y)`
- `GameObject:setWorldRotation(…)`
- `GameObject:setWorldRotationAngles(x, y, z)`
- `GameObject:setWorldRotationAnglesWithOrder(x, y, z, order)`
- `GameObject:spawn(name)`

## GoromorgBrainComponent (BrainComponent)

Implements AI for Goromorgs.

## GoromorgShieldComponent (Component)

Implements the Goromorg shield effect for monsters. The shielded monster is invulnerable to all damage. Instead the damage is directed to the shield. When the shield’s energy is depleted the shield is destroyed.

- `GoromorgShieldComponent:getEnergy()`
- `GoromorgShieldComponent:setEnergy(number)`

## GraphicsContext

- `GraphicsContext.button(id, x, y, width, height)`
- `GraphicsContext.color(r, g, b, a)`
- `GraphicsContext.drawImage(image, x, y)`
- `GraphicsContext.drawImage2(image, x, y, srcX, srcY, srcWidth, srcHeight, destWidth, destHeight)`
- `GraphicsContext.drawParagraph(text, x, y, width)`
- `GraphicsContext.drawRect(x, y, width, height)`
- `GraphicsContext.drawText(text, x, y)`
- `GraphicsContext.font(font)`
- `GraphicsContext.keyDown(key)`
- `GraphicsContext.mouseDown(button)`
- `GraphicsContext.width`
- `GraphicsContext.height`
- `GraphicsContext.mouseX`
- `GraphicsContext.mouseY`

## GravityComponent (Component)

Makes the object fall unless it is on ground or supported by a surface or a platform.

- `GravityComponent:getDestroySelf()`	Get whether component should be destroyed when it impacts ground
- `GravityComponent:getFallingSpeed()`
- `GravityComponent:isFalling()`
- `GravityComponent:setDestroySelf(boolean)`	Set whether component should be destroyed when it impacts ground
- `GravityComponent:setFallingSpeed(speed)`

## HealthComponent (Component)

Makes the object breakable. Typically used with Obstacle component to make breakable obstacles. When the health value reaches zero, the object is destroyed.

- `HealthComponent:getDieSound()`
- `HealthComponent:getHealth()`
- `HealthComponent:getImmunities()`
- `HealthComponent:getInvulnerable()`	Get whether the object is invulnerable to all damage
- `HealthComponent:getSpawnOnDeath()`
- `HealthComponent:setDieSound(string)`
- `HealthComponent:setHealth(number)`
- `HealthComponent:setImmunities(table)`
- `HealthComponent:setInvulnerable(boolean)`	Set whether the object is invulnerable to all damage
- `HealthComponent:setSpawnOnDeath(string)`
- `HealthComponent.onDie(self)`

## HeightmapComponent (Component)

## HerderBigBrainComponent (BrainComponent)

Implements AI for Big Herders.

## HerderSmallBrainComponent (BrainComponent)

Implements AI for Small Herders.

## IceGuardianBrainComponent (BrainComponent)

Implements AI for Ice Guardians.

## IceLizardBrainComponent (BrainComponent)

Implements AI for Ice Lizards.

## IceShardsComponent (Component)

Implements the Ice Shards spell.

- `IceShardsComponent:getDelay()`
- `IceShardsComponent:getRange()`
- `IceShardsComponent:grantTemporaryImmunity(GameObject, number)`
- `IceShardsComponent:setDelay(number)`
- `IceShardsComponent:setRange(number)`

## ItemActionComponent (Component)

Base-class for item actions (usually attacks). onAttack hook is called when the item’s action is performed by an champion.

- `ItemActionComponent:getBuildup()`	Get power attack buildup time (default 1 second)
- `ItemActionComponent:getChainAction()`
- `ItemActionComponent:getChainActionDelay()`
- `ItemActionComponent:getCooldown()`
- `ItemActionComponent:getEnergyCost()`
- `ItemActionComponent:getGameEffect()`
- `ItemActionComponent:getNextChainAction()`
- `ItemActionComponent:getRepeatCount()`
- `ItemActionComponent:getRepeatDelay()`
- `ItemActionComponent:getRequirements()`	Get list of skill requirements, e.g. { `two_handed`, 1, `axes`, 3 }
- `ItemActionComponent:getRequirementsText()`
- `ItemActionComponent:getUiName()`	Get power attack name
- `ItemActionComponent:setBuildup(number)`	Set power attack buildup time (default 1 second)
- `ItemActionComponent:setChainAction(string)`
- `ItemActionComponent:setChainActionDelay(number)`
- `ItemActionComponent:setCooldown(number)`
- `ItemActionComponent:setEnergyCost(number)`
- `ItemActionComponent:setGameEffect(string)`
- `ItemActionComponent:setRepeatCount(number)`
- `ItemActionComponent:setRepeatDelay(number)`
- `ItemActionComponent:setRequirements(table)`	Set list of skill requirements, e.g. { `two_handed`, 1, `axes`, 3 }
- `ItemActionComponent:setUiName(string)`	Set power attack name
- `ItemActionComponent.onAttack(self, champion, slot, chainIndex)`

## ItemComponent (Component)

Makes the object an item that can be picked up, dropped, thrown and placed into champions’ hands and inventory. Requires Model component.

- `ItemComponent:addTrait(trait)`
- `ItemComponent:getAchievement()`	Get achievement unlocked when the item is first picked up
- `ItemComponent:getArmorSet()`	Get the name of the armor set the item belongs to
- `ItemComponent:getCharges()`
- `ItemComponent:getConvertToItemOnImpact()`
- `ItemComponent:getDescription()`	Get textual description of the item
- `ItemComponent:getFitContainer()`	Get whether the item fits inside containers such as sacks or wooden boxes (default true)
- `ItemComponent:getFormattedName()`
- `ItemComponent:getFragile()`
- `ItemComponent:getFuel()`
- `ItemComponent:getGameEffect()`
- `ItemComponent:getGfxAtlas()`	Get filename of the icon texture
- `ItemComponent:getGfxIndex()`	Get index of icon in texture atlas
- `ItemComponent:getGfxIndexInHand()`	Get index of in-hand icon
- `ItemComponent:getGfxIndexPowerAttack()`	Get index of charging power attack icon
- `ItemComponent:getImpactSound()`	Get sound which is played when projectile item hits wall or a wall is hit with melee attack
- `ItemComponent:getJammed()`
- `ItemComponent:getMultiple()`	Get minimum count of items for splitting stacks
- `ItemComponent:getPrimaryAction()`	Get name of the component to trigger when item is clicked in the attack panel
- `ItemComponent:getProjectileRotationSpeed()`
- `ItemComponent:getProjectileRotationX()`
- `ItemComponent:getProjectileRotationY()`
- `ItemComponent:getProjectileRotationZ()`
- `ItemComponent:getSecondaryAction()`	Get name of the component to trigger when it’s secondary action is used
- `ItemComponent:getSharpProjectile()`	Get whether the item sticks to monsters on impact when thrown
- `ItemComponent:getStackSize()`
- `ItemComponent:getStackable()`	Get whether the item is stackable
- `ItemComponent:getTotalWeight()`
- `ItemComponent:getUiName()`	Get the name shown to the player
- `ItemComponent:getWeight()`	Get weight of the item in kilograms
- `ItemComponent:hasTrait(trait)`
- `ItemComponent:removeTrait(trait)`
- `ItemComponent:setAchievement(string)`	Set achievement unlocked when the item is first picked up
- `ItemComponent:setArmorSet(string)`	Set the name of the armor set the item belongs to
- `ItemComponent:setCharges(number)`
- `ItemComponent:setConvertToItemOnImpact(string)`
- `ItemComponent:setDescription(string)`	Set textual description of the item
- `ItemComponent:setFitContainer(boolean)`	Set whether the item fits inside containers such as sacks or wooden boxes (default true)
- `ItemComponent:setFragile(boolean)`
- `ItemComponent:setFuel(number)`
- `ItemComponent:setGameEffect(string)`
- `ItemComponent:setGfxAtlas(string)`	Set filename of the icon texture
- `ItemComponent:setGfxIndex(number)`	Set index of icon in texture atlas
- `ItemComponent:setGfxIndexInHand(number)`	Set index of in-hand icon
- `ItemComponent:setGfxIndexPowerAttack(number)`	Set index of charging power attack icon
- `ItemComponent:setImpactSound(string)`	Set sound which is played when projectile item hits wall or a wall is hit with melee attack
- `ItemComponent:setJammed(boolean)`
- `ItemComponent:setMultiple(number)`	Set minimum count of items for splitting stacks
- `ItemComponent:setPrimaryAction(string)`	Set name of the component to trigger when item is clicked in the attack panel
- `ItemComponent:setProjectileRotationSpeed(number)`
- `ItemComponent:setProjectileRotationX(number)`
- `ItemComponent:setProjectileRotationY(number)`
- `ItemComponent:setProjectileRotationZ(number)`
- `ItemComponent:setSecondaryAction(string)`	Set name of the component to trigger when it’s secondary action is used
- `ItemComponent:setSharpProjectile(boolean)`	Set whether the item sticks to monsters on impact when thrown
- `ItemComponent:setStackSize(count)`
- `ItemComponent:setStackable(boolean)`	Set whether the item is stackable
- `ItemComponent:setTraits(traits)`
- `ItemComponent:setUiName(string)`	Set the name shown to the player
- `ItemComponent:setWeight(number)`	Set weight of the item in kilograms
- `ItemComponent:updateBoundingBox()`
- `ItemComponent.onThrowAttackHitMonster(self, monster)`
- `ItemComponent.onEquipItem(self, champion, slot)`
- `ItemComponent.onUnequipItem(self, champion, slot)`

## ItemConstrainBoxComponent (Component)

## ItemSlot

- `ItemSlot.Weapon = 1`
- `ItemSlot.OffHand = 2`
- `ItemSlot.Head = 3`
- `ItemSlot.Chest = 4`
- `ItemSlot.Legs = 5`
- `ItemSlot.Feet = 6`
- `ItemSlot.Cloak = 7`
- `ItemSlot.Necklace = 8`
- `ItemSlot.Gloves = 9`
- `ItemSlot.Bracers = 10`
- `ItemSlot.Weapon2 = 11`
- `ItemSlot.OffHand2 = 12`
- `ItemSlot.BackpackFirst = 13`
- `ItemSlot.BackpackLast = 32`
- `ItemSlot.MaxSlots = 32`

## LadderComponent (Component)

## LensFlareComponent (Component)

## LeverComponent (Component)

A controller component that implements lever mechanics for an object. The GameObject should have a Clickable and an Animation component with `activate` and `deactivate` animation clips attached to it.

- `LeverComponent:getDisableSelf()`
- `LeverComponent:getSound()`
- `LeverComponent:isActivated()`
- `LeverComponent:isDeactivated()`
- `LeverComponent:setDisableSelf(boolean)`
- `LeverComponent:setSound(string)`
- `LeverComponent:setState(state)`
- `LeverComponent:toggle()`
- `LeverComponent.onActivate(self)`
- `LeverComponent.onDeactivate(self)`
- `LeverComponent.onToggle(self)`

## LightComponent (Component)

Dynamic light source for rendering. A single GameObject can have multiple Light components.

- `LightComponent:fadeIn(time)`
- `LightComponent:fadeOut(time)`
- `LightComponent:getBrightness()`
- `LightComponent:getCastShadow()`
- `LightComponent:getClipDistance()`
- `LightComponent:getColor()`
- `LightComponent:getColor2()`
- `LightComponent:getColor3()`
- `LightComponent:getDebugDraw()`
- `LightComponent:getDestroyObject()`
- `LightComponent:getDirection()`
- `LightComponent:getDisableSelf()`
- `LightComponent:getFadeOut()`
- `LightComponent:getRange()`
- `LightComponent:getShadowMapSize()`
- `LightComponent:getSpotAngle()`
- `LightComponent:getSpotSharpness()`
- `LightComponent:getStaticShadowDistance()`
- `LightComponent:getStaticShadows()`
- `LightComponent:getType()`
- `LightComponent:setBrightness(brightness)`
- `LightComponent:setCastShadow(castShadow)`
- `LightComponent:setClipDistance(face, distance)`
- `LightComponent:setColor(color)`
- `LightComponent:setColor2(color)`
- `LightComponent:setColor3(color)`
- `LightComponent:setDebugDraw(debugDraw)`
- `LightComponent:setDestroyObject(boolean)`
- `LightComponent:setDirection(direction)`
- `LightComponent:setDisableSelf(boolean)`
- `LightComponent:setFadeOut(time)`
- `LightComponent:setRange(range)`
- `LightComponent:setShadowMapSize(size)`
- `LightComponent:setSpotAngle(angle)`
- `LightComponent:setSpotSharpness(sharpness)`
- `LightComponent:setStaticShadowDistance(number)`
- `LightComponent:setStaticShadows(boolean)`
- `LightComponent:setType(type)`
- `LightComponent.onUpdate(self)`

## LindwormBrainComponent (BrainComponent)

Implements AI for the Lindworm.

## LindwormChargeComponent (Component)

## LindwormFlyComponent (Component)

## LockComponent (Component)

A controller component that implements lock mechanics for an object. Requires Clickable component.

- `LockComponent:getOpenedBy()`
- `LockComponent:getSound()`
- `LockComponent:setOpenedBy(string)`
- `LockComponent:setSound(string)`
- `LockComponent.onActivate(self)`

## MagmaGolemBrainComponent (BrainComponent)

Implements AI for Magma Golems.

## Map

Contains all entities (also known as GameObjects) of a dungeon level. Map size is currently always 32 by 32.

- `Map:allEntities()`
- `Map:checkLineOfFire(number, number, number, number, number)`
- `Map:checkLineOfSight(number, number, number, number, number)`
- `Map:checkObstacle(GameObject, number)`
- `Map:checkObstacle2(GameObject, number, number, number, number)`
- `Map:entitiesAt(number, number)`
- `Map:getAdjacentLevel(number, number, number)`
- `Map:getAutomapTile(number, number)`
- `Map:getCeilingElevation(number, number)`
- `Map:getElevation(number, number)`
- `Map:getHeight()`
- `Map:getLevelCoord()`
- `Map:getModuleHeight()`
- `Map:getName()`
- `Map:getWidth()`
- `Map:isBlocked(x, y, elevation)`
- `Map:isObstacle(x, y, elevation)`
- `Map:isVisited()`
- `Map:isWall(x, y)`
- `Map:mapToWorld(x, y)`
- `Map:setAutomapTile(number, number, number)`
- `Map:worldToMap(pos)`

## MapGraphicsComponent (Component)

Adds custom graphics to the automap.

- `MapGraphicsComponent:getImage()`
- `MapGraphicsComponent:getOffset0()`
- `MapGraphicsComponent:getOffset1()`
- `MapGraphicsComponent:getOffset2()`
- `MapGraphicsComponent:getOffset3()`
- `MapGraphicsComponent:getRotate()`
- `MapGraphicsComponent:setImage(image)`
- `MapGraphicsComponent:setOffset0(vec)`
- `MapGraphicsComponent:setOffset1(vec)`
- `MapGraphicsComponent:setOffset2(vec)`
- `MapGraphicsComponent:setOffset3(vec)`
- `MapGraphicsComponent:setRotate(boolean)`

## MapMarkerComponent (Component)

Adds a marker with text on the automap.

- `MapMarkerComponent:getText()`
- `MapMarkerComponent:setText(string)`

## MaterialEx

Holds parameters of a rendering material. Materials can only be accessed from material definition’s onUpdate hooks.

- `MaterialEx:setParam(string, number)`
- `MaterialEx:setTexcoordScaleOffset(number, number, number, number)`
- `MaterialEx:setTexture(string, string)`

## MeleeAttackComponent (ItemActionComponent)

Implements melee attack action for items. Melee attacks can hit and damage a single target in front of the party.

- `MeleeAttackComponent:getAccuracy()`	Get optional accuracy bonus
- `MeleeAttackComponent:getAttackPower()`	Get attack power of the attack
- `MeleeAttackComponent:getAttackSound()`	Get name of the sound effect to play (default `swipe`)
- `MeleeAttackComponent:getBaseDamageStat()`	Get base statistic used for computing damage modifier (default `strength`)
- `MeleeAttackComponent:getCameraShake()`
- `MeleeAttackComponent:getCauseCondition()`
- `MeleeAttackComponent:getConditionChance()`
- `MeleeAttackComponent:getDamageType()`	Get damage type of the attack: `physical` (default), `cold`, `fire`, `poison` or `shock`
- `MeleeAttackComponent:getPierce()`	Get how many points of armor is bypassed by the attack
- `MeleeAttackComponent:getReachWeapon()`	Get a boolean flag, if enabled the weapon can be used to attack from the backrow
- `MeleeAttackComponent:getRequiredLevel()`
- `MeleeAttackComponent:getSkill()`
- `MeleeAttackComponent:getSwipe()`	Get name of the swipe animation to play (default `horizontal`)
- `MeleeAttackComponent:getUnarmedAttack()`
- `MeleeAttackComponent:setAccuracy(number)`	Set optional accuracy bonus
- `MeleeAttackComponent:setAttackPower(number)`	Set attack power of the attack
- `MeleeAttackComponent:setAttackSound(string)`	Set name of the sound effect to play (default `swipe`)
- `MeleeAttackComponent:setBaseDamageStat(string)`	Set base statistic used for computing damage modifier (default `strength`)
- `MeleeAttackComponent:setCameraShake(boolean)`
- `MeleeAttackComponent:setCauseCondition(string)`
- `MeleeAttackComponent:setConditionChance(number)`
- `MeleeAttackComponent:setDamageType(string)`	Set damage type of the attack: `physical` (default), `cold`, `fire`, `poison` or `shock`
- `MeleeAttackComponent:setPierce(number)`	Set how many points of armor is bypassed by the attack
- `MeleeAttackComponent:setReachWeapon(boolean)`	Set a boolean flag, if enabled the weapon can be used to attack from the backrow
- `MeleeAttackComponent:setRequiredLevel(number)`
- `MeleeAttackComponent:setSkill(string)`
- `MeleeAttackComponent:setSwipe(string)`	Set name of the swipe animation to play (default `horizontal`)
- `MeleeAttackComponent:setUnarmedAttack(boolean)`
- `MeleeAttackComponent.onPostAttack(self, champion, slot)`
- `MeleeAttackComponent.onHitMonster(self, monster, tside, damage, champion)`

## MeleeBrainComponent (BrainComponent)

Implements AI for generic (stupid) melee monsters.

## MersenneTwister

- `MersenneTwister.create(seed)`
- `MersenneTwister.random()`
- `MersenneTwister.randomInt(min, max)`

## MimicCameraAnimationComponent (Component)

## ModelComponent (Component)

3D model for rendering. A single GameObject can have multiple Model components.

- `ModelComponent:getBoundBox()`
- `ModelComponent:getCastShadow()`
- `ModelComponent:getDebugDraw()`
- `ModelComponent:getDissolveEnd()`
- `ModelComponent:getDissolveStart()`
- `ModelComponent:getEmissiveColor()`
- `ModelComponent:getMaterial()`
- `ModelComponent:getMaterialOverrides()`
- `ModelComponent:getModel()`
- `ModelComponent:getReflection()`
- `ModelComponent:getRenderHack()`
- `ModelComponent:getShadowLod()`
- `ModelComponent:getSortOffset()`
- `ModelComponent:getStaticShadow()`
- `ModelComponent:getStoreSourceData()`
- `ModelComponent:setBoundBox(desc)`
- `ModelComponent:setCastShadow(enable)`
- `ModelComponent:setDebugDraw(debugDraw)`
- `ModelComponent:setDissolveEnd(number)`
- `ModelComponent:setDissolveStart(number)`
- `ModelComponent:setEmissiveColor(color)`
- `ModelComponent:setMaterial(material)`
- `ModelComponent:setMaterialOverrides(map)`
- `ModelComponent:setModel(filename)`
- `ModelComponent:setReflection(boolean)`
- `ModelComponent:setRenderHack(hack)`
- `ModelComponent:setShadowLod(number)`
- `ModelComponent:setSortOffset(offset)`
- `ModelComponent:setStaticShadow(enable)`
- `ModelComponent:setStoreSourceData(boolean)`
- `ModelComponent:updateLods()`

## MonsterActionComponent (Component)

Implements a custom monster action. An action is always connected with an animation that controls when the action starts and ends. onBeginAction and onEndAction hooks are called when the action is started and ended. onAnimationEvent hook is called when an animation event is triggered.

- `MonsterActionComponent:getAnimation()`
- `MonsterActionComponent:getCooldown()`
- `MonsterActionComponent:setAnimation(string)`
- `MonsterActionComponent:setCooldown(number)`
- `MonsterActionComponent.onBeginAction(self)`
- `MonsterActionComponent.onEndAction(self)`
- `MonsterActionComponent.onAnimationEvent(self, event)`

## MonsterAttackComponent (MonsterActionComponent)

Implements a monster attack action. A monster can have more than one attacks.

- `MonsterAttackComponent:getAccuracy()`
- `MonsterAttackComponent:getAnimationSpeed()`
- `MonsterAttackComponent:getAnimations()`
- `MonsterAttackComponent:getAttackFromBehindAnimation()`
- `MonsterAttackComponent:getAttackPower()`
- `MonsterAttackComponent:getAttackType()`
- `MonsterAttackComponent:getCameraShake()`
- `MonsterAttackComponent:getCameraShakeDuration()`
- `MonsterAttackComponent:getCameraShakeIntensity()`
- `MonsterAttackComponent:getCauseCondition()`
- `MonsterAttackComponent:getChangeFacing()`
- `MonsterAttackComponent:getConditionChance()`
- `MonsterAttackComponent:getDirection()`
- `MonsterAttackComponent:getImpactSound()`
- `MonsterAttackComponent:getKnockback()`
- `MonsterAttackComponent:getMaxDistance()`
- `MonsterAttackComponent:getMinDistance()`
- `MonsterAttackComponent:getProjectileHeight()`
- `MonsterAttackComponent:getProjectileOriginNode()`
- `MonsterAttackComponent:getReach()`
- `MonsterAttackComponent:getRepeatChance()`
- `MonsterAttackComponent:getScreenEffect()`
- `MonsterAttackComponent:getShootProjectile()`
- `MonsterAttackComponent:getSound()`
- `MonsterAttackComponent:getTurnToAttackDirection()`
- `MonsterAttackComponent:resetCooldown()`
- `MonsterAttackComponent:setAccuracy(number)`
- `MonsterAttackComponent:setAnimationSpeed(number)`
- `MonsterAttackComponent:setAnimations(anims)`
- `MonsterAttackComponent:setAttackFromBehindAnimation(string)`
- `MonsterAttackComponent:setAttackPower(number)`
- `MonsterAttackComponent:setAttackType(string)`
- `MonsterAttackComponent:setCameraShake(boolean)`
- `MonsterAttackComponent:setCameraShakeDuration(number)`
- `MonsterAttackComponent:setCameraShakeIntensity(number)`
- `MonsterAttackComponent:setCauseCondition(table)`
- `MonsterAttackComponent:setChangeFacing(number)`
- `MonsterAttackComponent:setConditionChance(number)`
- `MonsterAttackComponent:setDirection(number)`
- `MonsterAttackComponent:setImpactSound(string)`
- `MonsterAttackComponent:setKnockback(boolean)`
- `MonsterAttackComponent:setMaxDistance(number)`
- `MonsterAttackComponent:setMinDistance(number)`
- `MonsterAttackComponent:setProjectileHeight(number)`
- `MonsterAttackComponent:setProjectileOriginNode(string)`
- `MonsterAttackComponent:setReach(number)`
- `MonsterAttackComponent:setRepeatChance(number)`
- `MonsterAttackComponent:setScreenEffect(string)`
- `MonsterAttackComponent:setShootProjectile(string)`
- `MonsterAttackComponent:setSound(string)`
- `MonsterAttackComponent:setTurnToAttackDirection(boolean)`
- `MonsterAttackComponent:startCooldown()`
- `MonsterAttackComponent.onAttack(self)`
- `MonsterAttackComponent.onAttackHit(self, champion)`
- `MonsterAttackComponent.onDealDamage(self, champion, damage)`

## MonsterChangeAltitudeComponent (Component)

## MonsterChargeComponent (Component)

Implements a monster charge action. When the action is started, it first plays the `chargeBegin` animation after which it alternates between `chargeContinue1` and `chargeContinue2` animations until the charge ends. Each animation moves the monster forward by one square.

- `MonsterChargeComponent:getAttackPower()`
- `MonsterChargeComponent:getCooldown()`
- `MonsterChargeComponent:getSound()`
- `MonsterChargeComponent:setAttackPower(number)`
- `MonsterChargeComponent:setCooldown(number)`
- `MonsterChargeComponent:setSound(string)`

## MonsterComponent (Component)

Makes the object a monster. Requires Model, Animation and a brain component. Most monsters (depending on the brain) also require MonsterMove, MonsterTurn and MonsterAttack components.

- `MonsterComponent:addItem(item)`
- `MonsterComponent:addTrait(trait)`
- `MonsterComponent:attack()`
- `MonsterComponent:die()`
- `MonsterComponent:dropAllItems()`
- `MonsterComponent:getCapsuleHeight()`
- `MonsterComponent:getCapsuleRadius()`
- `MonsterComponent:getCollisionRadius()`
- `MonsterComponent:getCurrentAction()`
- `MonsterComponent:getDeathEffect()`
- `MonsterComponent:getDieSound()`
- `MonsterComponent:getEvasion()`
- `MonsterComponent:getExp()`
- `MonsterComponent:getFlying()`
- `MonsterComponent:getFootstepSound()`
- `MonsterComponent:getGroupSize()`
- `MonsterComponent:getHeadRotation()`	Get head node rotation for stun effect
- `MonsterComponent:getHealth()`
- `MonsterComponent:getHitEffect()`
- `MonsterComponent:getHitSound()`
- `MonsterComponent:getIdleAnimation()`
- `MonsterComponent:getImmunities()`
- `MonsterComponent:getLevel()`
- `MonsterComponent:getLootDrop()`
- `MonsterComponent:getMaxHealth()`
- `MonsterComponent:getMeshName()`
- `MonsterComponent:getMonsterFlag(string)`
- `MonsterComponent:getProtection()`
- `MonsterComponent:getResistance()`
- `MonsterComponent:getShape()`
- `MonsterComponent:getSwarm()`
- `MonsterComponent:hasTrait(trait)`
- `MonsterComponent:isAlive()`
- `MonsterComponent:isChangingAltitude()`
- `MonsterComponent:isFalling()`
- `MonsterComponent:isGroupLeader()`
- `MonsterComponent:isIdle()`
- `MonsterComponent:isImmuneTo(effect)`
- `MonsterComponent:isInBackRow()`
- `MonsterComponent:isInvulnerable()`
- `MonsterComponent:isMoving()`
- `MonsterComponent:isPerformingAction(name)`
- `MonsterComponent:isReadyToAct()`
- `MonsterComponent:knockback(direction)`
- `MonsterComponent:moveBackward()`
- `MonsterComponent:moveForward()`
- `MonsterComponent:performAction(name)`
- `MonsterComponent:removeItem(item)`
- `MonsterComponent:removeTrait(trait)`
- `MonsterComponent:setAIState(state)`
- `MonsterComponent:setCapsuleHeight(number)`
- `MonsterComponent:setCapsuleRadius(number)`
- `MonsterComponent:setCollisionRadius(number)`
- `MonsterComponent:setCondition(condition)`
- `MonsterComponent:setDeathEffect(string)`
- `MonsterComponent:setDieSound()`
- `MonsterComponent:setEvasion(number)`
- `MonsterComponent:setExp(number)`
- `MonsterComponent:setFlying(boolean)`
- `MonsterComponent:setFootstepSound(string)`
- `MonsterComponent:setHeadRotation(vec)`	Set head node rotation for stun effect
- `MonsterComponent:setHealth(health)`
- `MonsterComponent:setHitEffect(string)`
- `MonsterComponent:setHitSound(string)`
- `MonsterComponent:setIdleAnimation(string)`
- `MonsterComponent:setImmunities(immunities)`
- `MonsterComponent:setLevel(level)`
- `MonsterComponent:setLootDrop(table)`
- `MonsterComponent:setMaxHealth(health)`
- `MonsterComponent:setMeshName(string)`
- `MonsterComponent:setMonsterFlag(string, boolean)`
- `MonsterComponent:setProtection(number)`
- `MonsterComponent:setResistances(resists)`
- `MonsterComponent:setShape(shape)`
- `MonsterComponent:setSwarm(boolean)`
- `MonsterComponent:setTraits(traits)`
- `MonsterComponent:shootProjectile(projectile, height, attackPower)`
- `MonsterComponent:showDamageText(text)`
- `MonsterComponent:strafeLeft()`
- `MonsterComponent:strafeRight()`
- `MonsterComponent:throwItem(item, height, attackPower)`
- `MonsterComponent:turnLeft()`
- `MonsterComponent:turnRight()`
- `MonsterComponent.onProjectileHit(self, item, damage, damageType)`
- `MonsterComponent.onPerformAction(self, name)`
- `MonsterComponent.onDamage(self, damage, damageType)`
- `MonsterComponent.onDie(self)`

## MonsterDropItemComponent (Component)

## MonsterGroupComponent (Component)

Spawns a group of monsters when the next time the level is updated.

- `MonsterGroupComponent:getAIState()`
- `MonsterGroupComponent:getCount()`
- `MonsterGroupComponent:getLevel()`
- `MonsterGroupComponent:getMonsterType()`
- `MonsterGroupComponent:setAIState(state)`
- `MonsterGroupComponent:setCount(number)`
- `MonsterGroupComponent:setLevel(number)`
- `MonsterGroupComponent:setMonsterType(string)`
- `MonsterGroupComponent:spawnNow()`

## MonsterJumpComponent (Component)

## MonsterKnockbackComponent (Component)

## MonsterLightCullerComponent (Component)

## MonsterMoveAttackComponent (Component)

## MonsterMoveComponent (Component)

Implements low level movement behavior for monsters.

- `MonsterMoveComponent:getAnimationSpeed()`
- `MonsterMoveComponent:getAnimations()`
- `MonsterMoveComponent:getCooldown()`
- `MonsterMoveComponent:getDashChance()`
- `MonsterMoveComponent:getMoveBackwardAnimation()`
- `MonsterMoveComponent:getMoveForwardAnimation()`
- `MonsterMoveComponent:getResetBasicAttack()`
- `MonsterMoveComponent:getSound()`
- `MonsterMoveComponent:getStrafeLeft()`
- `MonsterMoveComponent:getStrafeLeftAnimation()`
- `MonsterMoveComponent:getStrafeRight()`
- `MonsterMoveComponent:getStrafeRightAnimation()`
- `MonsterMoveComponent:getTurnDir()`
- `MonsterMoveComponent:setAnimationSpeed(number)`
- `MonsterMoveComponent:setAnimations(anims)`
- `MonsterMoveComponent:setCooldown(number)`
- `MonsterMoveComponent:setDashChance(number)`
- `MonsterMoveComponent:setMoveBackwardAnimation(string)`
- `MonsterMoveComponent:setMoveForwardAnimation(string)`
- `MonsterMoveComponent:setResetBasicAttack(boolean)`
- `MonsterMoveComponent:setSound(string)`
- `MonsterMoveComponent:setStrafeLeft(boolean)`
- `MonsterMoveComponent:setStrafeLeftAnimation(string)`
- `MonsterMoveComponent:setStrafeRight(boolean)`
- `MonsterMoveComponent:setStrafeRightAnimation(string)`
- `MonsterMoveComponent:setTurnDir(number)`
- `MonsterMoveComponent.onUnlinkMonsterGroup(self)`

## MonsterOperateDeviceComponent (Component)

## MonsterPickUpItemComponent (Component)

## MonsterStealWeaponComponent (Component)

## MonsterTurnComponent (Component)

Implements low level turning behavior for monsters.

- `MonsterTurnComponent:getAnimationSpeed()`
- `MonsterTurnComponent:getAnimations()`
- `MonsterTurnComponent:getCooldown()`
- `MonsterTurnComponent:getResetBasicAttack()`
- `MonsterTurnComponent:getSound()`
- `MonsterTurnComponent:getTurnAroundAnimation()`
- `MonsterTurnComponent:getTurnLeftAnimation()`
- `MonsterTurnComponent:getTurnRightAnimation()`
- `MonsterTurnComponent:setAnimationSpeed(number)`
- `MonsterTurnComponent:setAnimations(anims)`
- `MonsterTurnComponent:setCooldown(number)`
- `MonsterTurnComponent:setResetBasicAttack(boolean)`
- `MonsterTurnComponent:setSound(string)`
- `MonsterTurnComponent:setTurnAroundAnimation(anim)`
- `MonsterTurnComponent:setTurnLeftAnimation(anim)`
- `MonsterTurnComponent:setTurnRightAnimation(anim)`

## MonsterWarpComponent (Component)

## MosquitoSwarmBrainComponent (BrainComponent)

Implements AI for Mosquito Swarms.

## NullComponent (Component)

## ObstacleComponent (Component)

Blocks movement for party and monsters. Optionally prevents placing items into obstacle’s square. Use the Health component to make the obstacle breakable.

- `ObstacleComponent:getBlockItems()`	Get whether items can be dropped to obstacle’s square
- `ObstacleComponent:getBlockMonsters()`	Get whether the obstacle blocks monster movement
- `ObstacleComponent:getBlockParty()`	Get whether the obstacle blocks party movement
- `ObstacleComponent:getHitEffect()`	Get particle effect to play when obstacle is hit
- `ObstacleComponent:getHitSound()`	Get sound to play when obstacle is hit
- `ObstacleComponent:getRepelProjectiles()`	Get whether impacted projectiles should be pushed out of obstacle’s square
- `ObstacleComponent:setBlockItems(boolean)`	Set whether items can be dropped to obstacle’s square
- `ObstacleComponent:setBlockMonsters(boolean)`	Set whether the obstacle blocks monster movement
- `ObstacleComponent:setBlockParty(boolean)`	Set whether the obstacle blocks party movement
- `ObstacleComponent:setHitEffect(string)`	Set particle effect to play when obstacle is hit
- `ObstacleComponent:setHitSound(string)`	Set sound to play when obstacle is hit
- `ObstacleComponent:setRepelProjectiles(boolean)`	Set whether impacted projectiles should be pushed out of obstacle’s square

## OccluderComponent (Component)

## OgreBrainComponent (BrainComponent)

Implements AI for Ogres.

## ParticleComponent (Component)

Adds a particle effect to the GameObject. A single GameObject can have multiple Particle components.

- `ParticleComponent:fadeIn(time)`
- `ParticleComponent:fadeOut(time)`
- `ParticleComponent:getDebugDraw()`
- `ParticleComponent:getDestroyObject()`	Get whether game object should be automatically destroyed when particle system is finished
- `ParticleComponent:getDestroySelf()`	Get whether particle component should be automatically destroyed when particle system is finished
- `ParticleComponent:getDisableSelf()`	Get whether particle component should be automatically disabled when particle system is finished
- `ParticleComponent:getEmitterMesh()`
- `ParticleComponent:getParticleSystem()`
- `ParticleComponent:getSortOffset()`
- `ParticleComponent:restart()`
- `ParticleComponent:setDebugDraw(boolean)`
- `ParticleComponent:setDestroyObject(boolean)`	Set whether game object should be automatically destroyed when particle system is finished
- `ParticleComponent:setDestroySelf(boolean)`	Set whether particle component should be automatically destroyed when particle system is finished
- `ParticleComponent:setDisableSelf(boolean)`	Set whether particle component should be automatically disabled when particle system is finished
- `ParticleComponent:setEmitterMesh(modelFile)`
- `ParticleComponent:setFadeOut(number)`
- `ParticleComponent:setParticleSystem(name)`
- `ParticleComponent:setSortOffset(offset)`
- `ParticleComponent:start()`
- `ParticleComponent:stop()`

## PartyComponent (Component)

The singular party component that holds the four champions. Champion’s position in the party can change when party formation is changed. However champions can be identified with their ordinal number that never changes.

- `PartyComponent:getChampion(index)`
- `PartyComponent:getChampionByOrdinal(ordinal)`
- `PartyComponent:grapple(time)`
- `PartyComponent:heal()`
- `PartyComponent:isCarrying(string)`
- `PartyComponent:isClimbing()`
- `PartyComponent:isFalling()`
- `PartyComponent:isMoving()`
- `PartyComponent:isResting()`
- `PartyComponent:knockback(direction)`
- `PartyComponent:playScreenEffect(filename)`
- `PartyComponent:rest()`
- `PartyComponent:shakeCamera(…, number)`
- `PartyComponent:swapChampions(i, j)`
- `PartyComponent:wakeUp(restInterrupted)`
- `PartyComponent.onCastSpell(self, champion, spell)`
- `PartyComponent.onDamage(self, champion, damage, damageType)`
- `PartyComponent.onDie(self, champion)`
- `PartyComponent.onAttack(self, champion, action, slot)`
- `PartyComponent.onLevelUp(self, champion)`
- `PartyComponent.onReceiveCondition(self, champion, condition)`
- `PartyComponent.onDrawGui(self, context)`
- `PartyComponent.onDrawInventory(self, context, champion)`
- `PartyComponent.onDrawStats(self, context, champion)`
- `PartyComponent.onDrawSkills(self, context, champion)`
- `PartyComponent.onDrawTraits(self, context, champion)`
- `PartyComponent.onPickUpItem(self, item)`
- `PartyComponent.onProjectileHit(self, champion, item, damage, damageType)`
- `PartyComponent.onRest(self)`
- `PartyComponent.onWakeUp(self)`
- `PartyComponent.onTurn(self, direction)`
- `PartyComponent.onMove(self, direction)`

## PitComponent (Component)

Implements pit mechanics for an object. Non-flying monsters, items and party fall down to level below if the pit is open.

- `PitComponent:close()`
- `PitComponent:getState()`
- `PitComponent:isClosed()`
- `PitComponent:isOpen()`
- `PitComponent:open()`
- `PitComponent:setState(state)`
- `PitComponent:toggle()`

## PlatformComponent (Component)

## PoisonCloudAttackComponent (Component)

## PoisonedMonsterComponent (Component)

Implements the poisoned condition for monsters. A monster with the poisoned condition is dealt ongoing poisoned damage until the effect’s duration ends or the monster dies.

- `PoisonedMonsterComponent:getCausedByChampion()`
- `PoisonedMonsterComponent:setCausedByChampion(number)`

## PortalComponent (Component)

- `PortalComponent.onArrival(self)`

## ProjectileColliderComponent (Component)

Defines the collision box for projectile-object collisions. Walls, doors, monsters and the party are implicitly projectile colliders and do not need ProjectileCollider components.

- `ProjectileColliderComponent:getCollisionGroup()`	Get collision group for filtering unwanted collisions (default 1)
- `ProjectileColliderComponent:getDebugDraw()`
- `ProjectileColliderComponent:getSize()`
- `ProjectileColliderComponent:setCollisionGroup(number)`	Set collision group for filtering unwanted collisions (default 1)
- `ProjectileColliderComponent:setDebugDraw(boolean)`
- `ProjectileColliderComponent:setSize(size)`

## ProjectileComponent (Component)

Causes the object to fly towards its facing direction. When the projectile hits something its onProjectileHit hook is called.

- `ProjectileComponent:getAngularVelocity()`
- `ProjectileComponent:getAttackPower()`	Get piggy back data for projectile attacks and spells
- `ProjectileComponent:getCastByChampion()`
- `ProjectileComponent:getCollisionMask()`	Get collision mask for filtering unwanted collisions (default 1)
- `ProjectileComponent:getDestroyOnImpact()`	Get destroy game object on impact
- `ProjectileComponent:getFallingVelocity()`
- `ProjectileComponent:getGravity()`
- `ProjectileComponent:getHitEffect()`
- `ProjectileComponent:getRadius()`
- `ProjectileComponent:getSpawnOffsetY()`
- `ProjectileComponent:getVelocity()`
- `ProjectileComponent:pushForward()`
- `ProjectileComponent:setAngularVelocity(number)`
- `ProjectileComponent:setAttackPower(number)`	Set piggy back data for projectile attacks and spells
- `ProjectileComponent:setCastByChampion(boolean)`
- `ProjectileComponent:setCollisionMask(number)`	Set collision mask for filtering unwanted collisions (default 1)
- `ProjectileComponent:setDestroyOnImpact(boolean)`	Set destroy game object on impact
- `ProjectileComponent:setFallingVelocity(number)`
- `ProjectileComponent:setGravity(number)`
- `ProjectileComponent:setHitEffect(string)`
- `ProjectileComponent:setIgnoreEntity(ent)`
- `ProjectileComponent:setRadius(number)`
- `ProjectileComponent:setSpawnOffsetY(number)`
- `ProjectileComponent:setVelocity(number)`
- `ProjectileComponent.onProjectileHit(self, what, entity)`

## ProjectileImpactComponent (Component)

Implements custom hit reaction for a projectile hit. This component is obsolete and not used by the main campaign. Use an onProjectileHit hook in the Projectile component instead.

- `ProjectileImpactComponent.onHitEntity(self, entity)`
- `ProjectileImpactComponent.onHitMonster(self, monster)`
- `ProjectileImpactComponent.onHitParty(self, party)`

## PullChainComponent (Component)

## PushableBlockComponent (Component)

Implements pushable block mechanics for an object. The pushable block must be activated and it can only be pushed to squares with pushable block floors.

- `PushableBlockComponent:activate()`
- `PushableBlockComponent:deactivate()`
- `PushableBlockComponent:push(dir)`

## PushableBlockFloorComponent (Component)

Implements custom floor trigger for pushable blocks.

- `PushableBlockFloorComponent:activate()`
- `PushableBlockFloorComponent:deactivate()`
- `PushableBlockFloorComponent:getInitialState()`
- `PushableBlockFloorComponent:isActivated()`
- `PushableBlockFloorComponent:setInitialState(boolean)`
- `PushableBlockFloorComponent:toggle()`

## RangedAttackComponent (ItemActionComponent)

Implements missile attack action for items. Missile attacks require ammo that must be held in champion’s other hand.

- `RangedAttackComponent:getAmmo()`
- `RangedAttackComponent:getAttackPower()`
- `RangedAttackComponent:getAttackSound()`
- `RangedAttackComponent:getBaseDamageStat()`	Get base statistic used for computing damage modifier (default `dexterity`)
- `RangedAttackComponent:getDamageType()`	Get damage type of the attack: `physical` (default), `cold`, `fire`, `poison` or `shock`
- `RangedAttackComponent:getProjectileItem()`	Get (optional) projectile item type that ammo is converted to when shot
- `RangedAttackComponent:getRequiredLevel()`
- `RangedAttackComponent:getSkill()`
- `RangedAttackComponent:getSwipe()`
- `RangedAttackComponent:setAmmo(string)`
- `RangedAttackComponent:setAttackPower(number)`
- `RangedAttackComponent:setAttackSound(string)`
- `RangedAttackComponent:setBaseDamageStat(string)`	Set base statistic used for computing damage modifier (default `dexterity`)
- `RangedAttackComponent:setDamageType(string)`	Set damage type of the attack: `physical` (default), `cold`, `fire`, `poison` or `shock`
- `RangedAttackComponent:setProjectileItem(string)`	Set (optional) projectile item type that ammo is converted to when shot
- `RangedAttackComponent:setRequiredLevel(number)`
- `RangedAttackComponent:setSkill(string)`
- `RangedAttackComponent:setSwipe(string)`
- `RangedAttackComponent.onPostAttack(self, champion, slot)`

## RangedBrainComponent (BrainComponent)

Implements AI for generic (stupid) ranged monsters.

## RatlingBossBrainComponent (BrainComponent)

Implements AI for the Ratling Boss.

## ReloadFirearmComponent (Component)

## RopeToolComponent (Component)

## RunePanelComponent (Component)

## ScriptComponent (Component)

Custom Lua script component. The script code may be embedded inside the component or in an external file.

- `ScriptComponent:loadFile(filename)`
- `ScriptComponent:setSource(source)`

## ScriptControllerComponent (Component)

## ScrollItemComponent (Component)

Displays a piece of text or an image in item’s tooltip.

- `ScrollItemComponent:getScrollImage()`	Get image shown when the scroll is examined
- `ScrollItemComponent:getScrollText()`	Get text shown when the scroll is examined
- `ScrollItemComponent:getTextAlignment()`	Get text alignment, `center` or `left`
- `ScrollItemComponent:setScrollImage(string)`	Set image shown when the scroll is examined
- `ScrollItemComponent:setScrollText(string)`	Set text shown when the scroll is examined
- `ScrollItemComponent:setTextAlignment(string)`	Set text alignment, `center` or `left`

## SecretComponent (Component)

Implements secret mechanics for an object. When the secret component is activated, it playes the secret found sound and increments the `secrets_found` statistics. Each secret can be triggered only once.

- `SecretComponent:activate()`

## SkeletonArcherBrainComponent (BrainComponent)

Implements AI for Skeleton Archers.

## SkeletonCommanderBrainComponent (BrainComponent)

Implements AI for Skeleton Commanders.

## SkyComponent (Component)

Placing an object with Sky component into a level makes it an outdoor level. Rendering parameters such as view distance and fog are set for outdoor rendering. The Sky component animates the light component attached to the same object to simulate day-night cycle. There should be only one Sky per level.

- `SkyComponent:getAmbientIntensity()`
- `SkyComponent:getFarClip()`
- `SkyComponent:getFogColor1()`
- `SkyComponent:getFogColor2()`
- `SkyComponent:getFogColor3()`
- `SkyComponent:getFogMode()`
- `SkyComponent:getFogRange()`
- `SkyComponent:getSunColor1()`
- `SkyComponent:getSunColor2()`
- `SkyComponent:getSunColor3()`
- `SkyComponent:getTonemapSaturation()`
- `SkyComponent:setAmbientIntensity(number)`
- `SkyComponent:setFarClip(number)`
- `SkyComponent:setFogColor1(vec)`
- `SkyComponent:setFogColor2(vec)`
- `SkyComponent:setFogColor3(vec)`
- `SkyComponent:setFogMode(string)`
- `SkyComponent:setFogRange(table)`
- `SkyComponent:setSunColor1(vec)`
- `SkyComponent:setSunColor2(vec)`
- `SkyComponent:setSunColor3(vec)`
- `SkyComponent:setTonemapSaturation(number)`

## SleepingMonsterComponent (Component)

## SlimeBrainComponent (BrainComponent)

Implements AI for Slimes.

## SmallFishControllerComponent (Component)

## SocketComponent (Component)

An attachment point for items. Wall hooks, sconces, statue’s hand could be sockets. A socket can hold a single item.

- `SocketComponent:addItem(item)`
- `SocketComponent:count()`
- `SocketComponent:getDebugDraw()`
- `SocketComponent:getItem()`
- `SocketComponent:setDebugDraw(boolean)`
- `SocketComponent.onInsertItem(self, item)`
- `SocketComponent.onRemoveItem(self, item)`
- `SocketComponent.onAcceptItem(self, item)`

## SoundComponent (Component)

Dynamic sound source. A single GameObject can have multiple Sound components.

- `SoundComponent:fadeIn(time)`
- `SoundComponent:fadeOut(time)`
- `SoundComponent:getPitch()`
- `SoundComponent:getSound()`
- `SoundComponent:getSoundType()`
- `SoundComponent:getVolume()`
- `SoundComponent:play(sound)`
- `SoundComponent:setPitch(number)`
- `SoundComponent:setSound(name)`
- `SoundComponent:setSoundType(type)`
- `SoundComponent:setVolume(number)`
- `SoundComponent:stop()`

## SpawnerComponent (Component)

A Spawner dynamically spawns a new object when it’s activate method is called. After spawning an object the spawner goes into cooldown. After the cooldown time has elapsed, the spawner can be activated again.

- `SpawnerComponent:activate()`
- `SpawnerComponent:getCooldown()`
- `SpawnerComponent:getDisableSelf()`
- `SpawnerComponent:getMonsterLevel()`
- `SpawnerComponent:getSpawnedEntity()`
- `SpawnerComponent:setCooldown(number)`
- `SpawnerComponent:setDisableSelf(boolean)`
- `SpawnerComponent:setMonsterLevel(number)`
- `SpawnerComponent:setSpawnedEntity(string)`
- `SpawnerComponent.onActivate(self)`

## SpellScrollItemComponent (Component)

Displays the gesture and information about a spell in item’s tooltip.

- `SpellScrollItemComponent:getSpell()`
- `SpellScrollItemComponent:setSpell(string)`

## StairsComponent (Component)

Transports the party and thrown items to another location in the game world. The target can be either a level below to above (set with setDirection method) or any location (set with setTeleportTarget).

- `StairsComponent:getDirection()`
- `StairsComponent:getTeleportTarget()`
- `StairsComponent:setDirection(string)`
- `StairsComponent:setTeleportTarget(level, x, y, elevation)`

## StatisticsComponent (Component)

## StonePhilosopherControllerComponent (Component)

## StunnedMonsterComponent (Component)

## SurfaceComponent (Component)

A support for placing items. Altars, alcoves and chests are typically surfaces.

- `SurfaceComponent:addItem(item)`
- `SurfaceComponent:count()`
- `SurfaceComponent:getDebugDraw()`
- `SurfaceComponent:getSize()`
- `SurfaceComponent:setDebugDraw(boolean)`
- `SurfaceComponent:setSize(vec)`
- `SurfaceComponent.onInsertItem(self, item)`
- `SurfaceComponent.onRemoveItem(self, item)`

## SwarmBrainComponent (BrainComponent)

Implements AI for swarm monsters.

## TeleporterComponent (Component)

Transports the party, monsters, items and spells to another location in the game world.

- `TeleporterComponent:getSpin()`
- `TeleporterComponent:getTeleportTarget()`
- `TeleporterComponent:getTriggeredByItem()`
- `TeleporterComponent:getTriggeredByMonster()`
- `TeleporterComponent:getTriggeredByParty()`
- `TeleporterComponent:getTriggeredBySpell()`
- `TeleporterComponent:setSpin(spin)`
- `TeleporterComponent:setTeleportTarget(level, x, y, elevation)`
- `TeleporterComponent:setTriggeredByItem(boolean)`
- `TeleporterComponent:setTriggeredByMonster(boolean)`
- `TeleporterComponent:setTriggeredByParty(boolean)`
- `TeleporterComponent:setTriggeredBySpell(boolean)`

## TentacleBrainComponent (BrainComponent)

Implements AI for Tentacles.

## TentacleHideComponent (Component)

## ThornWallComponent (Component)

## ThrowAttackComponent (ItemActionComponent)

Implements throw attack action for items. When thrown, a Projectile component is dynamically created and added to the thrown item.

- `ThrowAttackComponent:getAttackPower()`
- `ThrowAttackComponent:getAttackSound()`
- `ThrowAttackComponent:getBaseDamageStat()`	Get base statistic used for computing damage modifier (default `strength`)
- `ThrowAttackComponent:getRequiredLevel()`
- `ThrowAttackComponent:getSkill()`
- `ThrowAttackComponent:getSwipe()`
- `ThrowAttackComponent:setAttackPower(number)`
- `ThrowAttackComponent:setAttackSound(string)`
- `ThrowAttackComponent:setBaseDamageStat(string)`	Set base statistic used for computing damage modifier (default `strength`)
- `ThrowAttackComponent:setRequiredLevel(number)`
- `ThrowAttackComponent:setSkill(string)`
- `ThrowAttackComponent:setSwipe(string)`
- `ThrowAttackComponent.onPostAttack(self, champion, slot)`

## TileDamagerComponent (Component)

A TileDamager damages party, monsters and obstacles in the same square when activated. TileDamagers can be one shot or cause damage as long as the target stays in the same space.

- `TileDamagerComponent:getAttackPower()`	Get strength of the attack
- `TileDamagerComponent:getCameraShake()`	Get whether camera should be shaked when party is hit
- `TileDamagerComponent:getCastByChampion()`	Get champion ordinal if the spell was cast by a champion
- `TileDamagerComponent:getDamageFlags()`	Get special damage flags
- `TileDamagerComponent:getDamageType()`	Get damage type of the attack: `physical`, `fire`, `cold`, `shock`, or `poison`
- `TileDamagerComponent:getDestroyObject()`	Get whether the game object with burst spell component should be destroyed when component is triggered
- `TileDamagerComponent:getRepeatCount()`
- `TileDamagerComponent:getRepeatDelay()`
- `TileDamagerComponent:getScreenEffect()`	Get name of the on-screen particle effect to play when party is hit
- `TileDamagerComponent:getSound()`	Get name of the sound effect to play
- `TileDamagerComponent:setAttackPower(number)`	Set strength of the attack
- `TileDamagerComponent:setCameraShake(boolean)`	Set whether camera should be shaked when party is hit
- `TileDamagerComponent:setCastByChampion(number)`	Set champion ordinal if the spell was cast by a champion
- `TileDamagerComponent:setDamageFlags(number)`	Set special damage flags
- `TileDamagerComponent:setDamageType(string)`	Set damage type of the attack: `physical`, `fire`, `cold`, `shock`, or `poison`
- `TileDamagerComponent:setDestroyObject(number)`	Set whether the game object with burst spell component should be destroyed when component is triggered
- `TileDamagerComponent:setRepeatCount(number)`
- `TileDamagerComponent:setRepeatDelay(number)`
- `TileDamagerComponent:setScreenEffect(string)`	Set name of the on-screen particle effect to play when party is hit
- `TileDamagerComponent:setSound()`	Set name of the sound effect to play
- `TileDamagerComponent.onHitChampion(self, champion)`
- `TileDamagerComponent.onHitMonster(self, monster)`
- `TileDamagerComponent.onHitObstacle(self, obstacle)`

## Time

- `Time.currentTime()`
- `Time.deltaTime()`
- `Time.systemTime()`

## TimerComponent (Component)

Timer component triggers its onActivate hook periodically. The timer inverval or period can be customized. Timers can act in one shot mode (disable self set) or running mode (disable self not set).

- `TimerComponent:getCurrentLevelOnly()`
- `TimerComponent:getDisableSelf()`
- `TimerComponent:getTimerInterval(number)`
- `TimerComponent:getTriggerOnStart()`
- `TimerComponent:pause()`
- `TimerComponent:setCurrentLevelOnly(boolean)`
- `TimerComponent:setDisableSelf(boolean)`
- `TimerComponent:setTimerInterval(number)`
- `TimerComponent:setTriggerOnStart(boolean)`
- `TimerComponent:start()`
- `TimerComponent:stop()`
- `TimerComponent.onActivate(self)`

## TinyCritterControllerComponent (Component)

Implements the animation and behavior of tiny critters such as beach crabs.

- `TinyCritterControllerComponent:getSpeed()`	Get speed
- `TinyCritterControllerComponent:getStrafing()`	Get strafing (true or false)
- `TinyCritterControllerComponent:setSpeed(number)`	Set speed
- `TinyCritterControllerComponent:setStrafing(boolean)`	Set strafing (true or false)

## ToadBrainComponent (BrainComponent)

Implements AI for Swamp Toads.

## TorchHolderControllerComponent (Component)

Controller for torch holders. Requires Socket, Light, Sound and Particle components. The controller automatically spawns a new torch at the start of a new game and places it into the Socket component.

- `TorchHolderControllerComponent:getHasTorch()`
- `TorchHolderControllerComponent:setHasTorch(boolean)`

## TorchItemComponent (Component)

Makes an item a torch that burns until it runs out of fuel.

- `TorchItemComponent:getFuel()`	Get fuel for torches and other light sources
- `TorchItemComponent:setFuel(number)`	Set fuel for torches and other light sources

## TricksterBrainComponent (BrainComponent)

Implements AI for the Trickster.

- `TricksterBrainComponent:setState(state)`
- `TricksterBrainComponent.onThinkSpecial(self)`

## TurtleBrainComponent (BrainComponent)

Implements AI for Turtles.

## TwigrootBrainComponent (BrainComponent)

Implements AI for Twigroots.

## UggardianBrainComponent (BrainComponent)

Implements AI for Uggardians.

## UggardianFlamesComponent (Component)

A flaming special effect for creatures. Requires Model component.

- `UggardianFlamesComponent:getEmitFromMaterial()`
- `UggardianFlamesComponent:getParticleSystem()`
- `UggardianFlamesComponent:setEmitFromMaterial(string)`
- `UggardianFlamesComponent:setParticleSystem(string)`
- `UggardianFlamesComponent:stop()`

## UsableItemComponent (Component)

Makes an item Usable by right-clicking on it.

- `UsableItemComponent:getCanBeUsedByDeadChampion()`
- `UsableItemComponent:getEmptyItem()`
- `UsableItemComponent:getNutritionValue()`	Get nutrition value, i.e. how much food is restored when item is consumed (range 0-1000)
- `UsableItemComponent:getRequirements()`
- `UsableItemComponent:getSound()`	Get sound to play when item is consumed
- `UsableItemComponent:setCanBeUsedByDeadChampion(boolean)`
- `UsableItemComponent:setEmptyItem(string)`
- `UsableItemComponent:setNutritionValue(number)`	Set nutrition value, i.e. how much food is restored when item is consumed (range 0-1000)
- `UsableItemComponent:setRequirements(table)`
- `UsableItemComponent:setSound(string)`	Set sound to play when item is consumed
- `UsableItemComponent.onUseItem(self, champion)`

## ViperRootBrainComponent (BrainComponent)

Implements AI for Viper Roots.

## WallTextComponent (Component)

Displays a piece of text in the center of the screen when the object is clicked on. Requires Clickable component.

- `WallTextComponent:getHeight()`
- `WallTextComponent:getWallText()`
- `WallTextComponent:setHeight(number)`
- `WallTextComponent:setWallText(string)`
- `WallTextComponent.onShowText(self)`
- `WallTextComponent.onDismissText(self)`

## WallTriggerComponent (Component)

A wall trigger is activated when a projectile hits a wall in the wall trigger’s square. The wall needs to have same facing as the wall trigger. When activated the wall trigger fires its onActivate hooks and connectors.

- `WallTriggerComponent:getEntityType()`
- `WallTriggerComponent:setEntityType(string)`
- `WallTriggerComponent.onActivate(self)`

## WargBrainComponent (BrainComponent)

Implements AI for the Wargs.

## WaterSurfaceComponent (Component)

Updates the reflection buffer of a water object. There should be max one water surface component per level. Water reflection is very heavy on performance so use it wisely.

- `WaterSurfaceComponent:getFogColor()`
- `WaterSurfaceComponent:getFogDensity()`
- `WaterSurfaceComponent:getPlaneY()`
- `WaterSurfaceComponent:getReflectionColor()`
- `WaterSurfaceComponent:getRefractionColor()`
- `WaterSurfaceComponent:setFogColor(vec)`
- `WaterSurfaceComponent:setFogDensity(number)`
- `WaterSurfaceComponent:setPlaneY(number)`
- `WaterSurfaceComponent:setReflectionColor(vec)`
- `WaterSurfaceComponent:setRefractionColor(vec)`

## WaterSurfaceMeshComponent (Component)

Collects all water tiles in the level and creates an animated mesh covering all the tiles.

- `WaterSurfaceMeshComponent:getMaterial()`
- `WaterSurfaceMeshComponent:getUnderwaterMaterial()`
- `WaterSurfaceMeshComponent:getWaterLevel()`
- `WaterSurfaceMeshComponent:setMaterial(string)`
- `WaterSurfaceMeshComponent:setUnderwaterMaterial(string)`

## WizardBrainComponent (BrainComponent)

Implements AI for the Wizard.

## XeloroidBrainComponent (BrainComponent)

Implements AI for Xeloroids.

## ZarchtonBrainComponent (BrainComponent)

Implements AI for Zarchtons.
