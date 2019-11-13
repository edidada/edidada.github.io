---
title: android source pointer
date: 2017-10-31 17:31:36
categories:
- Tech
tags:
- Linux
- Note
- Android Source

---
# android source pointer

## 总结

RefBase内部有一个指针指向实际对象，有一个weakref_impl类型的指针保存对象的强／弱引用计数、对象生命周期控制。

sp只有一个成员变量，用来保存实际对象，但这个实际对象内部已包含了weakref_impl *对象用于保存实际对象的引用计数。sp 管理一个对象指针时，对象的强、弱引用数同时加1，sp销毁时，对象的强、弱引用数同时减1。

wp中有两个成员变量，一个保存实际对象，另一个是weakref_impl *对象。wp管理一个对象指针时，对象的弱引用计数加1，wp销毁时，对象的弱引用计数减1。

weakref_impl中包含一个flag用于决定对象的生命周期是由强引用数控制还是由弱引用数控制：

1.当flag为0时，实际对象的生命周期由强引用数控制，weakref_impl *对象由弱引用数控制。

2.当flag为OBJECT_LIFETIME_WEAK时，实际对象的生命周期受弱引用数控制。

3.当flag为OBJECT_LIFETIME_FOREVER时，实际对象的生命周期由用户控制。

可以用extendObjectLifetime改变flag的值。

[参考网址](http://blog.csdn.net/u012124438/article/details/71075423)