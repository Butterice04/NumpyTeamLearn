### task01-1:
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
