### 1. autorun 为何在内部有被使用的属性时就会触发
1. 每一个observable的函数都会生成一个唯一值（id）， autorun 执行时，调用挂载函数将回调挂载，然后执行回调，此时被get 的属性就会被监听到，在监听函数中将挂载的回调push到缓存中与当前的id对应。
2.下次再发生set方法时，对应的属性的所有autorun 缓存函数，都将被执行 foreach

### 2. Observer包裹的组件为何只对依赖的属性更新时刷新
1. autorun 实现了点对点的更新，Observer包裹组件后，更新组件的方法由autorun 触发即可