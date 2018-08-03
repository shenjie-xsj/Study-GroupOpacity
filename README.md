# Study-GroupOpacity
### 为学习组透明而创建的项目
UIView可以设置alpha的属性来确定视图的透明度。CALayer可以设置opacity来确定图层的透明度。这两个属性都会影响到子视图或子图层。

于是产生问题：
当一个包含子视图的区域被设置了50%的透明度，那么显示出来的颜色将一半显示本区域颜色，另一半显示背景颜色，两半颜色合起来成为最终颜色，这个最终颜色看起来就有了透明的效果。
但是，因为透明设置会级联到子视图，那么子视图也具备了50%的透明度，那么子视图显示出来的颜色将有一半是子视图自身颜色，另一半是已经具有透明效果（混合色）的父视图最终颜色，于是，子视图的最终颜色看起来是75%的透明效果……

对于上面的问题，三种解决方案：
- 手动计算出子视图应该有的透明度并单独赋值。这有个弊端，就是一旦视图树层级过多，那么每一级子视图都得手动计算一遍对应的透明度，很麻烦。
- 通过设置Info.plist文件的UIViewGroupOpacity值为true，来开启组透明效果。只不过这个配置对于整个项目均生效，波及面比较广，如果存在某些视图不需要组透明效果，那么这就有点得不偿失。
- 通过对需要组透明的视图或图层设置其CALayer的shouldRasterize属性值为true来开启对应视图或图层的组透明效果。只不过这个配置需要设置rasterizationScale属性以避免出现透明部分像素化问题。
