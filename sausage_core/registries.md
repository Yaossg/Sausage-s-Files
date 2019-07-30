# SausageCore 注册机制

SausageCore 是一个巨大的模组开发轮子，其中的注册机制是极为重要的一环。

下面介绍的是 SausageCore 1.6-alpha 有关注册的内容。

## PART 1 对 Forge 注册机制的封装

### IBRegistryManager

物品（**I**tem）和方块（**B**lock）毫无疑问是组成 MC 世界最重要的“基础设施”，没有之一。大量物品方块的注册繁复，往往令人恼火，**IB**RegistryManager 就是致力于解决这个问题的。

首先在你的 Mod 主类，创建一个 IBRegistryManager 的实例，注意：应保证在 preInit 之前创建，因此静态 initializer 无疑是最好的选择

```
public static final IBRegistryManager IB = new IBRegistryManager(MODID, new CreativeTabs(MODID) {
		@Override
		public ItemStack getTabIconItem() {
			return new ItemStack(sausage);
		}
	});
```

我把新创建的 CreativeTabs 传入作为参数，仍然可以通过`IB.tab`来访问到它，它也可以是`null`，表示这个管理器中的物品和方块不加入任何一个标签。

接着，在 preInit 阶段，就可以进行物品和方块的注册了，先来说比较简单的物品吧：

```
IB.addItem("poop");
ItemChloroplast chloroplast = IB.addItem("chloroplast", new ItemChloroplast());
IB.addItemCM(chloroplast, (stack, tintIndex) -> {
	if(tintIndex == 0) {
		float v = Math.max(0.0F, (float) (1.0F - stack.getItem().getDurabilityForDisplay(stack)));
		return MathHelper.hsvToRGB(Math.max(v / 3F, 0.5F / 3F), Math.min(v * 2, 1), 1.0F);
	}
	return 0xFFFFFF;
});
IB.addItem("stone_bucket", new ItemCustomBucket(), IBRegistryManager.mappingBy("universal", "milk"));
```

第一行注册了一个物品poop，物品的实例是通过`new Item()`来创建的，这是为了方便最常见的材料注册。

第二行注册了并存下了chloroplast，物品是用户自定义的类。接在在第三行，我们为这个物品添加了**C**olor**M**ultiplier，不需要担心是客户端还是服务端，也不需要担心是在什么时候注册（实际上ColorMultiplier要到 init 阶段才会被注册）。这也是这个轮子的一大特点——**一站式完成一切工作，端无关，时间无关**

第三行注册了一个石桶，用到了本模组的另外一个轮子 ItemCustomBucket，这里不做过多的介绍了，只做最简单的使用——它在metadata为0的时候表示通用的桶，为1时表示牛奶桶。这里就出现了两个模型，这时候就需要自定义模型注册了。第三个参数接受的是`Consumer<Item>`，不过但多数情况下就一简单映射，直接调用管理器的有关静态方法就可以解决，这就是这个轮子的设计宗旨——**在保证灵活的情况下易用**

然后再加点方块：

```
IB.addBlock("ash", new BlockAsh());
IB.addBlock("toilet", new BlockToilet(), ItemToilet::new, mappingBy("water", "lava"));
IB.addOnlyBlock("crop", new BlockCrop())
```

与物品不同，方块没有默认的创建方式。如果有需要，也可以通过`addBlockCM`来注册ColorMultiplier。而第二行最后一个参数和物品的最后一个参数用途一样。

第二行第三个参数，用于指定`ItemBlock`的获取方式，默认是通过`ItemBlock::new`来完成。

第三行展示了如何注册一个没有对应物品的方块。目前还没有做与`ItemBlockSpecial`的支持。

就此，物品和方块的注册就完成了。

### FluidRegistryManager



> TODO：文章未完成