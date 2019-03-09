# Sausage Core

> 教程对应版本：1.2（未完成）

如果需要api，可以在[这里](./api)下载

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

#### 调试棒

让你在旧版本享受新版本的语法高亮！

有三个模式，对着空中`shift+右键`切换

分别是切换、方块、实体

第一种模式会把指向的方块状态进行切换，按住`shift`反向切换

第二种模式输出方块id、状态、已经实体附加值的NBT

第三种模式输出实体的id和NBT

## API

对于大多数api，用途都是不言而喻的，仅仅是观察可以知晓多数类和方法的用途

因此只做一些简略的介绍

### core

core包下的内容往往是被设计成易被继承或实现的类或接口

### util

util包下的内容往往是静态方法类，或者不常继承的实用工具类，或是与modding关系不大的类

下面推荐几个力作吧

#### `math.BufferedRandom`

`BufferedRandom` 是一个随机数生成器，但是通过缓存整数的方式提高`nextBoolean`等方法的效率

#### `explosion.ExExplosion`

高度自定义的爆炸类，还提供了一个builder，顺便说一句，请不要忘了同时在服务端和客户端调用！

#### `common.SausageUtils`

一些杂七杂八的util，所有方法都配有javadoc，简单实用！

#### `energy`

- `BasicEnergyStorage`

普通的能量储存，附带了许多实用的功能

- `DynamicEnergyStorage`

动态能量储存——根据所储存的能量多少决定IO的速度，有两个不同版本

#### `item`

- `ItemStackComparators`

一些用于比较`net.minecraft.item.ItemStack`的比较器，和一个builder，告别痛苦的物品堆比较！

- `ItemStackMatches`

一些匹配物品堆的方法

- `PortableItemStackHandler`
- `SingleItemStackHandler`

对forge的`ItemStackHandler`的加强

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

前两个缓存以等待时机单独调用注册方法，支持模型注册，第三个较为简单，故为直接注册

- `IModdedRegistry`
- `SausageRegistry`

对Collection(后者提供实现，是List)的简单封装，模组的配方等的注册表

#### `world.gen`

- `WorldGenBuilder`

适用于矿物生成的builder

#### 未来展望

将会有专门处理矿物辞典(oredict)和文本(text)的包