# Sausage Core

> A useful library and utilities for players and modders

## General

### Crafting Ingredient

`sausage_core` adds 2 kinds of `Ingredient`, They are `ItemWildcard` and `OreFilter`

`ItemWildcard`(`sausage_core:item_wildcard`) is just vanilla `minecraft:item`, but without the tag of data, so it matches any metadata

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

util包下的内容往往是静态方法类, 或者不常继承的实用工具类, 或是与modding关系不大的类

下面推荐几个力作吧

#### `math.BufferedRandom`

`BufferedRandom` 是一个随机数生成器, 但是通过缓存整数的方式提高nextBoolean等方法的效率

#### `explosion.ExExplosion`

高度自定义的爆炸类, 使用方法不言自明, 顺便说一句, 请不要忘了同时在服务端和客户端调用！

#### `common.SausageUtils`

一些杂七杂八的util, 所有方法都配有javadoc, 简单实用！

#### `energy`

- `BasicEnergyStorage`

普通的能量储存, 附带了许多实用的功能

- `DynamicEnergyStorage`

动态能量储存——根据所储存的能量多少决定IO的速度, 有两个不同版本

#### `item`

- `ItemStackComparators`

一些用于比较net.minecraft.item.ItemStack的比较器, 和一个builder, 告别痛苦的物品堆比较！

- `ItemStackMatches`

一些匹配物品堆的函数

- `PortableItemStackHandler`
- `SingleItemStackHandler`

对forge的ItemStackHandler的加强

#### `nbt`

- `NBTs`

一些封装简单的对NBT操作的简化

- `NBTFactory`

通过反射来序列化、反序列化NBT的反射项目

**未经实践, 慎用**

#### `registry`

- `FluidRegistryManager`
- `IBRegistryManager`
- `SoundRegistryManager`

注册流体、物品方块、声音的三个类

前两个缓存再单独调用注册方法, 第三个直接注册

前两个提供模型注册方法

- `IModdedRegistry`
- `SausageRegistry`

对Collection(后者提供实现，是List)的简单封装, 模组的配方等的注册表

#### `world.gen`

- `WorldGenBuilder`

适用于矿物生成的builder

#### Future Development

package of oredict and text