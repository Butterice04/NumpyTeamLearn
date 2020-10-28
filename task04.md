### task04：数学函数及逻辑函数

#### 向量化与广播
##### 向量化和广播这两个概念是 numpy 内部实现的基础。有了向量化，编写代码时无需使用显式循环。这些循环实际上不能省略，只不过是在内部实现，被代码中的其他结构代替。向量化的应用使得代码更简洁，可读性更强，也可以说使用了向量化方法的代码看上去更“Pythonic”。
###### 小黄碎碎念：看了上面这段话，我才“显式”的体会到numpy作为矩阵运算的科学计算包的特点，好迟钝。。总是需要清楚明白的说出来。

* 广播（Broadcasting）<br>
广播机制描述了 numpy 如何在算术运算期间处理具有不同形状的数组，让较小的数组在较大的数组上“广播”，以便它们具有兼容的形状。<br>
总结来说，广播的规则有三个：<br>
1、如果两个数组的维度数dim不相同，那么小维度数组的形状将会在左边补1。<br>
2、如果shape维度不匹配，但是有维度是1，那么可以扩展维度是1的维度匹配另一个数组；<br>
3、如果shape维度不匹配，但是没有任何一个维度是1，则匹配引发错误。<br>
举一个不匹配报错的栗子：<br>
`import numpy as np`<br>
`x = np.arange(4)`<br>
`y = np.ones(5)`<br>
`print(x.shape)  # (4,)`<br>
`print(y.shape)  # (5,)`<br>
`print(x + y)`<br>
`# ValueError: operands could not be broadcast together with shapes (4,) (5,)`<br><br>


#### 数学函数<br>

  * 算术运算<br>
  运算在位置相同的元素之间进行,或对每个元素做一次运算。<br>
  `numpy.add(x1, x2, *args, **kwargs)` <br>
  `numpy.subtract(x1, x2, *args, **kwargs) `<br>
  `numpy.multiply(x1, x2, *args, **kwargs) `<br>
  `numpy.divide(x1, x2, *args, **kwargs) `<br>
  `numpy.floor_divide(x1, x2, *args, **kwargs) `<br>
  `numpy.power(x1, x2, *args, **kwargs) `<br>
  `numpy.sqrt(x, *args, **kwargs) `<br>
  `numpy.square(x, *args, **kwargs)` <br><br>

  * 三角函数<br>
  运算在位置相同的元素之间进行,或对每个元素做一次运算。<br>
  `numpy.sin(x, *args, **kwargs) `<br>
  `numpy.cos(x, *args, **kwargs)` <br>
  `numpy.tan(x, *args, **kwargs) `<br>
  `numpy.arcsin(x, *args, **kwargs) `<br>
  `numpy.arccos(x, *args, **kwargs)` <br>
  `numpy.arctan(x, *args, **kwargs) `<br>

  * 指数和对数<br>
  运算在位置相同的元素之间进行,或对每个元素做一次运算。<br>
  `numpy.exp(x, *args, **kwargs) `<br>
  `numpy.log(x, *args, **kwargs)` <br>
  `numpy.exp2(x, *args, **kwargs) `<br>
  `numpy.log2(x, *args, **kwargs) `<br>
  `numpy.log10(x, *args, **kwargs)`<br><br>

  * 一些聚合函数<br>
    * 加法函数<br>
  `numpy.sum(a[, axis=None, dtype=None, out=None, …])`<br>
  通过不同的 axis，numpy 会沿着不同的方向进行操作，返回结果是一个数组，设axis=i，则 numpy 沿着第i个下标变化的方向进行操作；如果不设置，那么对所有的元素操作，返回结果是一个单值。<br>
    * 乘法函数<br>
    `numpy.cumsum(a, axis=None, dtype=None, out=None) `<br><br>
    * 乘积函数<br>
    `numpy.prod(a[, axis=None, dtype=None, out=None, …])`<br><br>
    * 累乘函数<br>
    `numpy.cumprod(a, axis=None, dtype=None, out=None) `<br><br>
    * 差值函数<br>
    `numpy.diff(a, n=1, axis=-1, prepend=np._NoValue, append=np._NoValue)` <br><br>
    a：输入矩阵<br>
    n：可选，代表要执行几次差值<br>
    axis：默认是最后一个<br>
    * 舍入函数(四舍五入)<br>
    `numpy.around(a, decimals=0, out=None)`<br><br>
    * 上下限函数<br>
    `numpy.ceil(x, *args, **kwargs) `<br>
    `numpy.floor(x, *args, **kwargs)`<br><br>
    * 取绝对值函数<br>
    `numpy.absolute(x, *args, **kwargs) `<br>
    `numpy.abs(x, *args, **kwargs)` <br><br>
    * 返回每个元素的符号，0返回0<br>
    `numpy.sign(x, *args, **kwargs)`<br><br>


#### 逻辑函数

* 真值测试<br>
`numpy.all(a, axis=None, out=None, keepdims=np._NoValue)`<br>
`numpy.any(a, axis=None, out=None, keepdims=np._NoValue)`<br><br>
  * 是否为空值<br>
  `numpy.isnan(x, *args, **kwargs)`<br><br>
* 逻辑运算<br>
`numpy.logical_not(x, *args, **kwargs)`<br>
`numpy.logical_and(x1, x2, *args, **kwargs)`<br>
`numpy.logical_or(x1, x2, *args, **kwargs)`<br>
`numpy.logical_xor(x1, x2, *args, **kwargs)`<br><br>
* 比较函数<br>
`numpy.greater(x1, x2, *args, **kwargs)`<br>
`numpy.greater_equal(x1, x2, *args, **kwargs)`<br>
`numpy.equal(x1, x2, *args, **kwargs)`<br>
`numpy.not_equal(x1, x2, *args, **kwargs)`<br>
`numpy.less(x1, x2, *args, **kwargs)`<br>
`numpy.less_equal(x1, x2, *args, **kwargs)`<br><br>
  * 比较两个数组的元素在一个可容忍范围内是否相等，返回布尔数组。<br>
  `numpy.isclose(a, b, rtol=1.e-5, atol=1.e-8, equal_nan=False)`<br><br> 
  * 同上，返回一个布尔值。<br>
  `numpy.allclose(a, b, rtol=1.e-5, atol=1.e-8, equal_nan=False)`<br><br>
  看一个有意思的栗子：<br>
  `x = np.isclose([1.0, np.nan], [1.0, np.nan])`<br>
  `print(x)  # [ True False]`<br><br>
  `x = np.isclose([1.0, np.nan], [1.0, np.nan], equal_nan=True)`<br>
  `print(x)  # [ True  True]`<br><br>
