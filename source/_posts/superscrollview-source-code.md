---
title: SuperScrollView 源代码
date: 2026-06-30 19:40:00
categories:
  - Unity
tags:
  - Unity
  - SuperScrollView
  - 源码阅读
description: 关于 SuperScrollView 对象池机制的一些源码阅读笔记。
---

## Q1：对象池的设计机制？

```csharp
Dictionary<string, ItemPool> mItemPoolDict = new Dictionary<string, ItemPool>();

List<ItemPool> mItemPoolList = new List<ItemPool>();
```

在 `LoopListItemPool.cs` 中设计了一个双层缓存池：

- `mPooledItemList`：正式池，存放已经完全失活、随时可以被拿出来重新使用的 Item。
- `mTmpPooledItemList`：临时池，是一个缓冲区。Item 刚被滑出屏幕，也就是 Viewport 回收时，先放进临时池，而不是立刻放进正式池直接执行 `SetActive(false)` 等操作。

## Init：预加载

在列表初始化时，会主动根据 `mInitCreateCount` 预先创建好一定数量的 Item 并放入池中。

创建的方法：`CreateItem()`

放入池中的方法：`RecycleItemReal()`

## CreateItem：根据预制体创建 Item

`CreateItem()` 负责根据预制体创建新的 Item。

## RecycleItem：将单个 Item 放入临时池

```csharp
item.Deactivate();
mTmpPooledItemList.Add(item);
```

这里不会直接 `SetActive(false)`，而是会用自身的 `Deactivate()` 方法取消激活。

## RecycleItemReal：将单个 Item 放入正式池

```csharp
void RecycleItemReal(LoopListViewItem2 item)
{
    item.Deactivate();
    item.gameObject.SetActive(false);
    mPooledItemList.Add(item);
}
```

## GetItem：从池子里获取 Item

`GetItem()` 会从池子里取出 Item，或者创建一个新的 Item。

1. `mCurItemIdCount++`。这一步很聪明：每一个 Item 都有不同的自增 ID，这个 ID 可以用来处理异步回调。比如异步加载网络图片时，由于对象池的存在，Item 会不断回收和重新拿出。图片加载发起时的 ID 和加载完成后现在的 ID 不一定一致。如果不一致，就说明 Item 已经被回收过并且借给别人了，这时不应该把图片显示出来，否则会出现图片错位的 bug。
2. 看临时池 `mTmpPooledItemList` 中有没有现成的 Item。有的话拿出最后一个 Item，并执行 `mTmpPooledItemList.RemoveAt(count - 1)`，让临时池数量减一，再将拿出的 Item 激活：`SetActive(true)`。
3. 如果临时池中没有，也就是 `count <= 0`，就看正式池。如果正式池的 count 也等于 0，就通过 `CreateItem()` 创建新的 Item；如果正式池中有 Item，就从正式池中取。

## ClearTmpRecycledItem：将临时池 Item 放入正式池

通过 `RecycleItemReal()` 方法将临时池内的 Item 放入正式池，然后清空临时池。

> 总结：这里用了两个池子，一个临时池，一个正式池，用双层对象池来处理 Item 的回收和复用。

## Q2：如何回收和复用对象池中的 Item？

待继续阅读源码。
