### CSS的各种单位

---

#### 单位类型
- absolute units
- font relative unit
- viewport relative  

#### absolute units
依赖确定的绝对值，不会被屏幕尺寸或者字体影响。由于它们依赖屏幕的DPI(dots per inch)，显示效果由不同的屏幕分辨率而有差异。

包括：

- px(pixels)
- in(inch)
- cm(centimeter)
- mm(millimeter)
- pc(picas)
- pt(points)

#### font relative units
- rem
  相对根元素html的`font-size`

- em
  相对当前元素`font-size`

- unitless value
  无单位的值一般用作`line-height`的值，相对于当前元素`font-size`

#### viewport relative units
- vh
  - 视窗高度
  - `1vh = 视窗高度/100`

- vw
  同理vh，视窗宽度

- vmax
  - `1vmax = max(vh, vw)/100`

- vmin
  - `1vmin = vim(vh, vw)/100`

#### percentage
- `width` `height`相对于父元素的`width` `height`
- `font-size`相对于父元素的`font-size`
- 特例：`padding` `margin`相对于父元素`width`（可用于保持宽高比，如`padding-top: 50%`）
- `line-height`相对于自身的`font-size`
- `vertical-align`相对于自身`line-height`



