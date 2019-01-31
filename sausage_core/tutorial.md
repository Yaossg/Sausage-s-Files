# Sausage Core

> A useful library and utilities for players and modders

## 常规

### 合成配方

`sausage_core`加入了两种新的合成配方(`Ingredient`)，它们是`ItemWildcard`和`OreFilter`

`ItemWildcard`(`sausage_core:item_wildcard`)就是原版的`minecraft:item`，但是没有data标签，所以匹配任意的metadata

`OreFilter`(`sausage_core:ore_filter`)根据谓词匹配矿物辞典，可以使用以下谓词

- `startsWith`
- `endsWith`
- `contains`
- `matches`
- `equals`
- `equalsIgnoreCase`

如

	{
		"predicate": "startsWith",
		"argument": "ingot"
	}

匹配所有锭

### 世界类型

`sausage_core`加入了2种世界类型(`WorldType`)

`Buffet`是低配版的(1.13)自选世界，可以选择一个生物群系，生成一个整个世界都是这个生物群系的世界。自定义页面下有三个按钮，左按钮上一个生物群系，右按钮下一个生物群系，中间按钮会在mod之间切换（如目前是mod A的生物群系，点一下就切换到第一个mod B的生物群系）

`CustomSize`是自定义生物群系大小的世界

#### 未来展望

`ChaosBiomes`

### 物品

#### 香肠

作者，吉祥物，不健康的食物

#### 信息卡

右键获取一些信息

## API

对于大多数api，用途都是不言而喻的，仅仅是观察可以知晓多数类和方法的用途

因此只做一些简略的介绍

### core

core包下的内容往往是被设计成易被继承或实现的类或接口

### util

util包下的内容往往是静态方法类，或者不常继承的实用工具类，或是与modding关系不大的类

下面推荐几个力作吧

#### `math.BufferedRandom`

`BufferedRandom` 是一个随机数生成器，但是通过缓存整数的方式提高nextBoolean等方法的效率

#### `explosion.ExExplosion`

高度自定义的爆炸类，使用方法不言自明，顺便说一句，请不要忘了同时在服务端和客户端调用！

#### `common.SausageUtils`

一些杂七杂八的util，所有方法都配有javadoc，简单实用！

#### `energy`

- `BasicEnergyStorage`

普通的能量储存，附带了许多实用的功能

- `DynamicEnergyStorage`

动态能量储存——根据所储存的能量多少决定IO的速度，有两个不同版本

#### `item`

- `ItemStackComparators`

一些用于比较net.minecraft.item.ItemStack的比较器，和一个builder，告别痛苦的物品堆比较！

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

**未经实践，慎用**

#### `registry`

- `FluidRegistryManager`
- `IBRegistryManager`
- `SoundRegistryManager`

注册流体、物品方块、声音

前两个缓存再单独调用注册方法，第三个直接注册

前两个提供模型注册方法

- `IModdedRegistry`
- `SausageRegistry`

对Collection(后者提供实现，是List)的简单封装，模组的配方等的注册表

#### `world.gen`

- `WorldGenBuilder`

适用于矿物生成的builder

#### 未来展望

将会有专门处理矿物辞典(oredict)和文本(text)的包