# SausageCore 注册机制

SausageCore 是一个巨大的模组开发轮子，其中的注册机制是极为重要的一环。

下面介绍的是 SausageCore 1.6-alpha 有关注册的内容。

## PART A 对 Forge 注册机制的封装

### IBRegistryManager

物品（**I**tem）和方块（**B**lock）毫无疑问是组成 MC 世界最重要的“基础设施”，没有之一。大量物品方块的注册繁复，往往令人恼火，**IB**RegistryManager 就是致力于解决这个问题的。

首先在你的 Mod 主类，创建一个`IBRegistryManager`的实例。注意：应保证在 preInit 之前创建，因此静态 initializer 无疑是最好的选择。

```
public static final IBRegistryManager IB = new IBRegistryManager(MODID,
			new ItemGroup(MODID, () -> new ItemStack(sausage)));
```

`ItemGroup`是`CreativeTabs`的子类，我把新创建标签的作为参数传入，仍然可以通过`IB.tab`来访问到它，它也可以是`null`，表示这个管理器中的物品和方块不加入任何一个标签。

接着，在 preInit 阶段，就可以进行物品和方块的注册了，先来说比较简单的物品吧：

```
IB.addItem("poop");
IB.addItem("stone_bucket", new ItemCustomBucket(), IItemML.mappingBy("universal", "milk"));
ItemChloroplast chloroplast = IB.addItem("chloroplast", new ItemChloroplast());
IB.addItemCM(chloroplast, IItemCM.mappingBy(stack -> {
	float v = Math.max(0.0F, (float) (1.0F - stack.getItem().getDurabilityForDisplay(stack)));
	return MathHelper.hsvToRGB(Math.max(v / 3F, 0.5F / 3F), Math.min(v * 2, 1), 1.0F);
}));

```

第一行注册了一个物品 poop，物品的实例是通过`new Item()`来创建的，这是为了方便最常见的材料注册。默认的注册的模型的 variant 叫 `"inventory"`。

第二行注册了一个石桶，用到了本模组的另外一个轮子`ItemCustomBucket`，这里不做过多的介绍了，只做最简单的使用——它在 metadata 为 0 的时候表示通用的桶，为 1 时表示牛奶桶。这就需要自定义模型注册了。第三个参数接受的是`IItemML`（物品模型加载器，**ItemM**odel**L**oader）。

第三行注册了并存下了 chloroplast，接在在第四行，我们为这个物品添加了`IItemCM`（物品颜色倍增器，**ItemC**olor**M**ultiplier），让它在 100% -> 50% 耐久时由绿变黄，50% -> 0% 耐久时由黄变灰。

你或许注意到了：**不需要担心**是在什么阶段注册（**何时**），也**不需要担心**是客户端还是服务端（**何地**）。**“一站式，集中化”**是本轮子的一大亮点。

你或许还注意到了，`IItemML` 和 `IItemCM` 都是**函数式接口**，这会非常方便你用任何你喜欢的方式表达你要完成的任务，这是**灵活性**。但是大多数情况下，我们所需要做的仅仅是对有限的情况进行机械匹配 ，因此我还提供了相关的静态方法，用来构造一些实用的实例，这是**易用性**。二者之结合就是这个轮子的设计宗旨——**在保证灵活的情况下易用**。

然后再加点方块：

```
IB.addBlock("ash", new BlockAsh());
IB.addBlock("toilet", new BlockToilet(), ItemToilet::new, IItemML.mappingBy("water", "lava"));
IB.addOnlyBlock("crop", new BlockCrop())
```

与物品不同，方块没有默认的创建方式。类似地，也可以通过`addBlockCM`来注册`IBlockCM`（方块颜色倍增器，**BlockC**olor**M**ultiplier），传入最后一个参数作为物品模型加载器。

第二行第三个参数，用于指定`ItemBlock`的获取方式，默认是通过`ItemBlock::new`来完成。

第三行展示了如何注册一个没有对应物品的方块。目前还没有做与`ItemBlockSpecial`的支持。

就此，物品和方块的注册就完成了。

### FluidRegistryManager

流体（**Fluid**）是MC中除物品之外最重要的物质材料，也是 Forge 的“最伟大的杰作之一”。杰作必须要打引号，Forge 拥有化神奇为腐朽的能力。面对流体，初学者总是焦头烂额，就连老手也要处处提防。本模组只做了一点微小的工作——通过 **Fluid**RegistryManager 简化流体注册。

首先在你的 Mod 主类，创建一个`FluidRegistryManager`的实例。注意：应保证在 preInit 之前创建，因此静态 initializer 无疑是最好的选择。

```
public static final Fluid steam = FLUID.register(new FluidSteam());
public static final Fluid methane = FLUID.register(new FluidMethane(), BlockCombustibleGas::new);
```

上面的代码应写在一个特定的类，并在preInit阶段加载这个类。

第一行注册了一个普通的流体，无对应方块。第二行注册了一个带方块的流体。

如果`FluidRegistry.isUniversalBucketEnabled() == true`，那么Forge 的 UniversalBucket 也会被添加。

### SoundRegistryManager

不废话了，这个轮子用法很简单。直接放源码：

```
public class SoundRegistryManager {
	public final String modid;
	public SoundRegistryManager(String modid) { this.modid = modid; }
	public SoundEvent register(String name) { 
		ResourceLocation soundName = new ResourceLocation(modid, name);
		SoundEvent soundEvent = new SoundEvent(soundName);
		ForgeRegistries.SOUND_EVENTS.register(soundEvent.setRegistryName(soundName));
		return soundEvent;
	}
}
```

看一眼就会用了嘛。