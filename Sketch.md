通用的图层使用 symbol 实现。

shared style 在 layer list 的图标颜色是灰色和紫色边框。

如果要对齐一个特定的对象，首先将该 layer 锁定，通过 左边 layer 的 icon，或 shift + commond + L。如果没有锁定的 layer，默认以所选中的 layer 最外层为标准

# Shapes

## Boolean Operations

通过组合基础图形可以创造复杂图形。

### subpaths

所有图形的可以用点来形成连接，实现不同的形状，这些点的集合称为 path。

图形可以有多个 subpath，图形的现实效果取决于这些 subpath 如何组合 (通过 boolean operation) 。

在 sketch 中进行 boolean operation 时，会将最顶层的图形作为第二高图形的 subpath 并使用特定的 boolean operation。

因为 sketch 进行 boolean operation 是动态计算的所以你可以实时调整 subpath，例如你的图形之一是矩形，你可以为单独的 subpath 调整边角角度。


## Operations

Union：组合两个图形的区域。
Subtract:顶部的图形与底部被覆盖的区域都移除
Intersect:保留相交区域，移除不相交区域
Difference:移除相交区域，保留不相交区域
