### task02-1:索引与切片
&emsp;&emsp;副本与视图：在 Numpy 中，做数组运算或数组操作时，返回结果不是数组的副本就是视图。
* 赋值运算不创建副本
   创建副本的函数：`numpy.ndarray.copy()` <br>例：`y=x.copy()`<br>
* 数组切片返回的是视图。<br><br>

#### 索引与切片
  * 整数索引：
  `x[2]` `x[2,1]` `x[2][1]`<br>

  * 切片索引<br>
  &emsp;&emsp;切片操作是指抽取(或查看)数组的一部分元素生成新数组。<br>
  &emsp;&emsp;对 python 列表进行切片操作得到的数组是原数组的**副本**，而对 Numpy 数据进行切片操作得到的数组则是指向相同缓冲区的**视图**。<br><br>
  &emsp;&emsp;用法：`x[start:stop:step]`，其中，第二个冒号可以省略。<br>
  &emsp;&emsp;三个位置为空时，即取默认值，start的默认值为0，stop的默认值为数组的最大索引值，可以用`-1`指示，step的默认值为1。取值为负数时，方向为逆向，即从后往前数。<br>
  &emsp;&emsp;可以用`x[:]`索引数组全部元素，用`x[-1]`取最后一个元素，用`x[::-1]`逆向取所有元素。其中，`x`为数组名。<br><br>
  **注意！python中的区间都是前闭后开的，用切片举例，得到的数组视图包含start，不包含stop。**<br><br>
  &emsp;&emsp;二维数组类似，稍有不同处实操一波就能理解。<br>
  例如，取所有元素的两种方式 `x[:]` `x[:, :]` 逗号隔开的，前一部分表示对行的处理，后一部分对列。<br><br>

  * dots索引<br>
  &emsp;&emsp;NumPy 允许使用 ... 表示足够多的冒号来构建完整的索引列表。<br>
  比如，x是一个5维数组，有：<br>
    1. x[1,2,...] 等于 x[1,2,:,:,:] <br>
    2. x[...,3] 等于 x[:,:,:,:,3] <br>
    3. x[4,...,5,:] 等于 x[4,:,:,5,:]<br><br>

  * 整数数组索引<br>
  方括号内放入多个索引值，可以索引多个元素，可以理解为无规律的自选索引值，任选多个指定位置的元素。<br>可与切片操作结合使用。<br><br>
  例：<br>
  `x = np.array([[1,2,3,4,5],`<br>
  `[6,7,8,9,10],`<br>
  `[11,12,13,14,15],`<br>
  `[16,17,18,19,20],`<br>
  `[21,22,23,24,25]])`<br><br>
  `print(x[::3,::2])`<br>
  `# [[ 1  3  5] `<br>
  `#  [16 18 20]]`<br><br>
  `print(x[1::3,::2])`<br>
  `# [[ 6  8 10]`<br>
  `#  [21 23 25]]`<br><br>

    注意,索引值必须先存在数组里：<br>
    `print(x[1,2]) # 8`<br><br>
    `a=[1,2]`<br>
    `print(x[a])`<br>
    `# [[ 6  7  8  9 10]`<br>
    `#  [11 12 13 14 15]]`<br><br>
  搭配方式很多，还可以对列表做同样的操作进行对比，需实操体会，难以一一言传。<br>
  一些练习写在[task02.ipynb](https://github.com/Butterice04/NumpyTeamLearn/blob/main/task02.ipynb)里啦。<br><br>
    * 一个函数，可以用axis指定行或列,axis=0表示以`indices`作为索引操作**行**取`a`的元素，axis=1表示操作**列**。<br>
  `numpy.take( a, indices, axis=None, out=None, mode='raise')`<br><br>

* 布尔索引<br>
意思是索引值是布尔类型的，可以是单个布尔值，也可以是一个布尔数组，true表示选中，false表示不选，可以用一些判断函数(的结果)作为索引值，进行筛选。<br><br>
举个小栗子：<br>
`x = np.array([1, 2, 3, 4, 5, 6, 7, 8])`
`y = x > 5 `<br>
`print(y) `<br>
`# [False False False False False  True  True  True] `<br>
`print(x[y]) `<br>
`# [6 7 8]`<br><br>

#### 数组迭代
一个优雅的遍历函数：<br>
`numpy.apply_along_axis(func1d, axis, arr)`<br>
举栗子在[task02.ipynb](https://github.com/Butterice04/NumpyTeamLearn/blob/main/task02.ipynb)里啦
