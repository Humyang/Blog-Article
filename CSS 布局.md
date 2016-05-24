## flex

flex-grow，当 flex children 未占满 flex container 时可以使用这个属性提升 flex children 所占比例
flex-shrink, 缩小 flex children 所占比例，即便 flex children 已经占满 flex container

使用  ` flex-basis: 7em;` 保证元素拥有最小宽度，配合 `flex-grow: 1;` 加大其它元素宽度。
例如一个元素内有两个子元素，各占 50% 宽度，只有左边一个时占 100% 的宽度。先设置左边的宽度为 100%，然后设置右边的 flex-basis:100%; 即可



低版本安卓元素默认高度过高，试试设置容器高度。

低版本的 flex (display:box)  布局，如果 justify 无效，试试将子元素的 display 设置为 block。
