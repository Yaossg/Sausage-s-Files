# 关于空指针的检验

```
   Objects.requireNonNull();   
   Preconditions.checkNotNull();
```

首先我会第一时间用**后者**，一方面是因为后者自带简易的错误信息**格式化**，那玩意效率要比`String.format`高，而对于错误信息来说足够了，另一方便是**统一化**倒向谷歌（因为Preconditions类还有**其他的检查器**）

其次，我们来看

```
a.f()
Objects.requireNonNull(a).f()
```

为什么我会说这样的检验完全没有意义？因为如果a是null，两者的效果是**完全一样**的

那么来看这个例子

```
class A {
	Bar bar;
	A(Bar bar) {
		this.bar = Preconditions.checkNotNull(bar);
	}
	
	void apply() {
		bar.foo();	
	}
}
```

为什么这里需要一个null的检验？因为很明显，如果不作检验，这个问题的发现会被**延迟**，直到apply被调用，我们才得知出现了致命的错误，可是来源在呢？我们无从知晓。这才是**验空的意义**。