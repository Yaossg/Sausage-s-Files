# Sausage Core

> A useful library and utilities for players and modders

## General

For api, you can download [HERE](./api)

### Crafting Ingredient

`sausage_core` adds 2 kinds of `Ingredient`, They are `ItemWildcard` and `OreFilter`

`ItemWildcard`(`sausage_core:item_wildcard`) is literally `minecraft:item`, but with no tag of data, so it matches any metadata

`OreFilter`(`sausage_core:ore_filter`) matches ore dictionary according to predicate, predicates you can use are:

- `startsWith`
- `endsWith`
- `contains`
- `matches`
- `equals`
- `equalsIgnoreCase`

e.g.

	{
		"predicate": "startsWith",
		"argument": "ingot"
	}

matches any ingot

### World Type

`sausage_core` adds 2 `WorldType`s

`Buffet` is minimal (1.13) buffet world, you can select a biome, which covers the entire world. There are 3 buttons in the customize page, the left one is 'previous biome', the one on the right is 'next biome', the one between them is used to switch among mods
(e.g. If a biome in Mod A is being selected currently, clicking the button will cause the first one in Mod B to be selected)

`CustomSize` is a world type in which you can customize biome size

#### Future Development

`ChaosBiomes` More Chaos More Fun!

### Items

#### Sausage

author, mascot, unhealthy food

#### Info Card

right click to get some information

## API

For most api, its usage is self-evident by just viewing its code of classes and methods

so there's only some simple description

### core

entries in package core is designed as classes or interface easy to be extended or implemented

### util

entries in package util provides classes with static methods and unlikely extended classes, or even just utils that does not relate to modding

here are some recommended great ones

#### `math.BufferedRandom`

`BufferedRandom` is a RNG, but buffers integer to improve performance of  methods like `nextBoolen `
#### `explosion.ExExplosion`

highly recommend explosion class, with a builder, by the way, don't forget calling this on both side of server and client!

#### `common.SausageUtils`

some misc utils, each of them has javadoc, simple but useful!

#### `energy`

- `BasicEnergyStorage`

normal energy storage, with a lot of useful functions

- `DynamicEnergyStorage`

dynamic energy storage, whose I/O speed depends on its energy stored. 2 different types.

#### `item`

- `ItemStackComparators`

some comparator `net.minecraft.item.ItemStack`, with a builder, just say goodbye to painful item stack comparison!

- `ItemStackMatches`

methods that match item stack

- `PortableItemStackHandler`
- `SingleItemStackHandler`

enhanced forge's `ItemStackHandler`

#### `nbt`

- `NBTs`

simple boxes for simplifying NBT operations

- `NBTFactory`

project of serialize and deserialize NBT by reflection

**No Practice Present, Take Care**

#### `registry`

- `FluidRegistryManager`
- `IBRegistryManager`
- `SoundRegistryManager`

register fluids/items & blocks/sounds

the first two buffer their entries in order to wait the time to register at other place and support model loading. the third one registers directly since it is simple

- `IModdedRegistry`
- `SausageRegistry`

easy box on Collection(the latter on List), registry for modding recipes and so on

#### `world.gen`

- `WorldGenBuilder`

builder mainly used in ore generations

#### Future Development

package of oredict and text