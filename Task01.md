### task01-1:常量 & 数据类型 & 时间日期
* 常量<br>
NAN、INF、pi、e

* 数据类型<br>
bool、int、float、str、datatime64（日期时间）、timedelta64（时间间隔）<br>
  * bool<br>
  8位,bool8
  * int<br>
  8位，int8=byte，一个字节；<br>16位，int16=short；<br>32位；<br>64位，int64=long=int0。<br>此外还有无符号整型uint，有对应的8/16/32/64位。
  * float<br>
  16位；<br>32位；<br>64位，float64=double (double在这里噢)
  * str<br>
  unicode=str0
  * datatime64
  * timedelta64
  在np.array中加入字段`dtype=xxx`如`dtype=datatime64`可以指定数据类型。<br>

* 创建数据类型(直接给出实例)<br>
(b表示bool型，1表示一个字节大小)<br>
`a=np.dtype('b1')`<br>
`print(a.type)  # <class 'numpy.bool_'>`<br>
`print(a.itemsize)  # 1`<br><br>
(int型有i1/i2/i4/i8)<br>
`b=np.dtype('i4')`<br>
`print(a.type)  # <class 'numpy.int32'>`<br>
`print(a.itemsize)  # 4`<br><br>
((byte-)string,S3表示长度为3的字符串)<br>
`c=np.dtype('S3')`<br>
`print(a.type)  # <class 'numpy.bytes_'>`<br>
`print(a.itemsize)  # 3`<br><br>
(Unicode字符串)<br>
`d=np.dtype('U3')`<br>
`print(a.type)  # <class 'numpy.str_'>`<br>
`print(a.itemsize)  # 12`<br><br>
  
* 数据类型信息<br>(也不知道是干啥的，可以求某个类型数的范围，float同)<br>
`ii32 = np.iinfo(np.int32)`<br>
`print(ii32.min)  # -2147483648`<br>
`print(ii32.max)  # 2147483647`<br><br>

* 时间日期(datatime64)<br>
  (datetime已被python包含的日期时间库所占用，datatime库中有datatime函数，可以与datatime64作类型转换)<br>
  `a = np.datetime64('2020-03-01')`<br>
  `print(a, a.dtype)  # 2020-03-01 datetime64[D]`<br>
  (D表示day，还有W，M，Y，s，m，h，年月日天大写，时分秒小写)<br>
  注1：从字符串创建 datetime64 类型时，默认情况下，numpy 会根据字符串自动选择对应的单位。<br><br>
  `a = np.datetime64('2020-03', 'D')` <br>
  `print(a, a.dtype)  # 2020-03-01 datetime64[D]`<br>
  (指定为Y就只有2020)<br>
  注2：从字符串创建 datetime64 类型时，可以强制指定使用的单位，如果指定的比写的长，长出来的部分默认最小单位，短则直接截断。<br><br>
  `print(np.datetime64('2020-03') == np.datetime64('2020-03-01'))  # True`<br>
  `print(np.datetime64('2020-03') == np.datetime64('2020-03-02'))  #False`<br>
  注3：一个比较的例子，numpy中，2020-03和2020-03-01实际上表示同一个时间。事实上，如果两个 datetime64 对象具有不同的单位，它们可能仍然代表相同的时刻。并且从较大的单位（如月份）转换为较小的单位（如天数）是安全的。<br><br>
  `a = np.arange('2020-08-01 20:00', '2020-08-10', dtype=np.datetime64)`<br>
  注4：用range()可以生成日期范围的数组，如果起始时间和结束时间单位不一样，统一化成小的那一个，如上例，转成分钟m。<br><br><br>
  补充：<br>
  小队群里有同学问了个问题，很有意思：<br>
  `a=np.datetime64('2020-10-19','W')`<br>
  `print(a, a.dtype) # 2020-10-15 datetime64[W]`<br><br>
  输出竟然是上一周的周四，然后我试了试其他日期(这里就只贴一个啦)：<br>
  `a=np.datetime64('2020-10-25','W')`<br>
  `print(a, a.dtype) # 2020-10-22 datetime64[W]`<br><br>
  然后发现，竟然每个都是输出某一个周四，还不是天数最近的周四(10-19是周一，离本周四只隔两天，10-15是上周四，隔了3天)，神奇！<br>
  突然我灵机一动，查了下1970年1月1日是周几，竟然就是周四！这一定不是巧合，于是我们猜测，这个周(W)是从周四开始算的，也就是周四的每周的“第一天”，那这样10-19还在10-15开始的“本周”就不奇怪了。所以我们的结论就是，如果指定类型为周(W)，返回的时间就是“上周四”！<br>
  如果不对，还请各位师傅指正，拜谢。<br><br>
  
* 时间增量(时间运算)<br>
  datatime64运算结果是timedelta64型的，单位不同时化成小的那个。<br>
  注意，年Y和月M不能和其他单位作运算，两者之间可以。(想想为什么?)<br>
  并且，除法运算的结果没有单位。<br>
  `a = np.timedelta64(1, 'Y')`<br>
  `b = np.timedelta64(6, 'M')`<br>
  `print(a+b) # 18 months`<br>
  `print(a/b) # 2.0`<br><br>
  
* numpy的busday(工作日)功能<br>
这里是学习手册原话：<br>
  * 将指定的偏移量应用于工作日，单位天（'D'）。计算下一个工作日，如果当前日期为非工作日，默认报错。可以指定 forward 或 backward 规则来避免报错。（一个是向前取第一个有效的工作日，一个是向后取第一个有效的工作日）。<br>
  * 可以指定偏移量为 0 来获取当前日期向前或向后近的工作日，当然，如果当前日期本身就是工作日，则直接返回当前日期。<br><br>
 
一开始没理解这两句话合起来什么效果，不明白为啥b是13号，然后多做了几个情况的输出，发现，应该是这样算的：如果指定了“forward”或“backward”，那么就会先偏移到`当前日期向前或向后近的工作日`(向前还是向后是指定规则决定的)，然后进行`工作日`的偏移。还是用b举例，因为是“backward”规则，所以向后找最近的工作日，也就是07-10，然后进行“1”个偏移，就是下一个工作日07-13，a 因为是“forward”向前偏移的，所以先定位到07-13，然后进行“1”个偏移，就是07-14。<br>
还有一个offsets取值的point，如果是正数就是向前偏移，负数就向后。<br><br>
内心os：理解了以后觉得之前的自己好傻，其实还是因为一开始没明白这个向前向后的规则，现在明白了写下来，以后就不会忘啦~<br><br>
  `# 2020-07-11 星期六`<br>
  `a = np.busday_offset('2020-07-11', offsets=1, roll='forward')`<br>
  `b = np.busday_offset('2020-07-11', offsets=1, roll='backward')`<br>
  `bb = np.busday_offset('2020-07-11', offsets=2, roll='backward')`<br> 
  `c = np.busday_offset('2020-07-11', offsets=-1, roll='backward')`<br> 
  `d = np.busday_offset('2020-07-11', offsets=0, roll='backward')`<br>
  `e = np.busday_offset('2020-07-11', offsets=0, roll='forward')`<br>
  `print(a) # 2020-07-14`<br>
  `print(b) # 2020-07-13`<br>
  `print(bb) # 2020-07-14`<br>
  `print(c) # 2020-07-09`<br>
  `print(d) # 2020-07-10`<br>
  `print(e) # 2020-07-13`<br><br>
  补充：<br>
更新一位师傅的原话(问题和解答,师傅很厉害,自己解决了)：<br>
Q:那为什么我一个backward参数还控制不了方向呢？需要把offsets改成-1才是找之前的工作日<br>
A:“backward”和“forward”不是控制方向，是改变基准日期，前移一天或者后移一天。<br><br>

### task01-2:数组
#### 关于numpy的数组，numpy 提供的重要的数据结构是 ndarray ，它是 python 中 list 的扩展。

* 创建数组<br>
  * 通过array()函数创建<br>
  `def array(p_object, dtype=None, copy=True, order='K', subok=False, ndmin=0): `<br>
  一维数组：`a = np.array([0, 1, 2, 3, 4])`，内层的方括号`[]`可换成圆括号`()`<br><br>
  二维数组：`b = np.array([[11, 12, 13, 14, 15],[16, 17, 18, 19, 20]])`，两个一位数组之间用逗号隔开。<br><br>
  其他维数也可创建。<br><br>
  * 通过asarray()函数进行创建<br>
  `def asarray(a, dtype=None, order=None):`<br>
        `return array(a, dtype, copy=False, order=order)`<br><br>
  可通过dtype指定数据类型。<br><br>
  `x = [[1, 1, 1], [1, 1, 1], [1, 1, 1]] `<br>
  `print(x,type(x)) # [[1, 1, 1], [1, 1, 2], [1, 1, 1]] <class 'list'>`<br>
  `y = np.asarray(x)`<br>
  `print(z,type(z))`<br>
  `# [[1 1 1] `<br>
  `#  [1 1 1] `<br>
  `#  [1 1 1]] <class 'numpy.ndarray'>`<br><br>
  * 通过fromfunction()函数进行创建(给函数绘图时可以用)<br>
  举个有意思的栗子：<br>
  `x = np.fromfunction(lambda i, j: i == j, (3, 3), dtype=int)`<br>
  `print(x)`<br>
  `# [[ True False False] `<br>
  `#  [False  True False] `<br>
  `#  [False False  True]] `<br><br>
  也可以自己def一个函数做运算生成array。<br><br>
  * 创建特别的数组(有的地方和MATLAB很像，我先学的MATLAB，所以这样说)<br>
    * 0数组：zeros()和zeros_like()<br><br>
    zeros()的参数是数组规格，如：<br>
    `x = np.zeros([2, 3]) `<br>
    `print(x) # [[0. 0. 0.] `<br>
    `#  [0. 0. 0.]] `<br><br>
    zeros_like()的参数是另一个数组，表示要生成一个形如参数的数组，如：<br>
    `x = np.array([[1, 2, 3], [4, 5, 6]])`<br>
    `y = np.zeros_like(x) `<br>
    `print(y) `<br>
    `# [[0 0 0] `<br>
    `#  [0 0 0]] `<br><br>
    * 1数组：ones()和ones_like()<br><br>
    同0数组，只是数组元素值全为1。<br><br>
    * 空数组：empty()和empty_like()<br><br>
    同0数组，只是数组元素值全为随机数。<br><br>
    * 单位数组：eye()和identity()<br><br>
    eye()：创建一个对角线上为1其他位置为0的数组，不一定是方形的。<br>
    `x = np.eye(4)`<br>
    `print(x) `<br>
    `# [[1. 0.] `<br>
    `#  [0. 1.]]`<br><br>
    `y = np.eye(2, 3)`<br>
    `print(y) `<br>
    `# [[1. 0. 0.] `<br>
    `#  [0. 1. 0.]]`<br><br>
    identity()保证是方形的。<br><br>
    * 对角数组<br><br>
    可以从一个数组中提取对角线(得到列表)，也可以从列表构造一个对角数组(其他位置元素值为0)。<br>
    有一个参数k，默认为0，表示对角线位置，1表示对角线上移一个单位，-1表示下移一个单位。可换成其他数字，数字绝对值表示步长，符号表示方向(跟我们的普遍认知是差不多哒~)。<br><br>
    * 常数数组：full()和full_like()<br><br>
    基本同0数组，在规格或数组后加一个常数参数即可，数组中的元素值都是这个常数。<br><br>
  * 利用数值范围创建<br>
  1. arange() 函数：返回给定间隔内的均匀间隔的值。 <br>
  2. linspace() 函数：返回指定间隔内的等间隔数字。 <br>
  3. logspace() 函数：返回数以对数刻度均匀分布。 默认以10为底，起点终点是指数部分的值，第三个参数是数组元素个数。<br>
  4. numpy.random.rand() 返回一个由[0,1)内的随机数组成的数组。<br><br>
  `x = np.logspace(0,5,10) `<br>
  `print(x)`<br>
  `# [1.00000000e+00 3.59381366e+00 1.29154967e+01 4.64158883e+01 1.66810054e+02 5.99484250e+02 2.15443469e+03 7.74263683e+03 2.78255940e+04 1.00000000e+05]`<br><br>
  * 创建结构数组<br>
    * 利用字典定义结构<br><br>
    `personType = np.dtype({    `<br>
    `'names': ['name', 'age', 'weight'],`<br>
    `'formats': ['U30', 'i8', 'f8']})`<br><br>
    `a = np.array([('Liming', 24, 63.9), ('Mike', 15, 67.), ('Jan', 34, 45.8)],dtype=personType) `<br><br>
    可以使用字段名作为下标获取对应的值：<br>
    `print(a['name']) `<br>
    `# ['Liming' 'Mike' 'Jan'] `<br><br>
* 数组的属性<br>
  1. numpy.ndarray.ndim 用于返回数组的维数（轴的个数）也称为秩，一维数组的秩为 1，二维数组的秩为 2，以此类推。<br>
  2. numpy.ndarray.shape 表示数组的维度，返回一个元组，这个元组的长度就是维度的数目，即 ndim 属性(秩)。<br>
  3. numpy.ndarray.size 数组中所有元素的总量，相当于数组的 shape 中所有元素的乘积，例如矩阵的元素总量为行与列的乘积。<br>
  4. numpy.ndarray.dtype ndarray 对象的元素类型。 5. numpy.ndarray.itemsize 以字节的形式返回数组中每一个元素的大小。<br><br>

    
