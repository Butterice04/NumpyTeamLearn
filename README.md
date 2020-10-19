# NumpyTeamLearn
datawhale十月组队学习:
[开源学习资料](https://github.com/datawhalechina/team-learning-program/tree/master/IntroductionToNumpy)<br><br>
ps.记得`import numpy as np`噢<br><br><br>
-----------[2020.10.19更新]-----------
### task01:
* 常量<br>
NAN、INF、pi、e

* 数据类型<br>
bool、int、float、str、datatime64（日期时间）、timedelta64（时间间隔）<br>
  * bool<br>
  8位,bool8
  * int<br>
  8位，int8=byte，一个字节；16位，int16=short；32位；64位，int64=long=int0。此外还有无符号整型uint，有对应的8/16/32/64位。
  * float<br>
  16位；32位；64位，float64=double (double在这里噢)
  * str<br>
  unicode=str0
  * datatime64
  * timedelta64
  在np.array中加入字段`dtype=xxx`如`dtype=datatime64`可以指定数据类型。<br>

* 创建数据类型(直接给出实例)<br>
`a=np.dtype('b1')`(b表示bool型，1表示一个字节大小)<br>
`print(a.type)  # <class 'numpy.bool_'>`<br>
`print(a.itemsize)  # 1`<br><br>
`b=np.dtype('i4')`(int型有i1/i2/i4/i8)<br>
`print(a.type)  # <class 'numpy.int32'>`<br>
`print(a.itemsize)  # 4`<br><br>
`c=np.dtype('S3')`((byte-)string,S3表示长度为3的字符串)<br>
`print(a.type)  # <class 'numpy.bytes_'>`<br>
`print(a.itemsize)  # 3`<br><br>
`d=np.dtype('U3')`(Unicode字符串)<br>
`print(a.type)  # <class 'numpy.str_'>`<br>
`print(a.itemsize)  # 12`<br><br>
  
* 数据类型信息<br>(也不知道是干啥的，可以求某个类型数的范围，float同)<br>
`ii32 = np.iinfo(np.int32)`<br>
`print(ii32.min)  # -2147483648`<br>
`print(ii32.max)  # 2147483647`<br><br>

* 时间日期
  * datatime64 <br>
  (datetime已被python包含的日期时间库所占用，datatime库中有datatime函数，可以与datatime64作类型转换)<br>
  `a = np.datetime64('2020-03-01')`<br>
  `print(a, a.dtype)  # 2020-03-01 datetime64[D]`<br>
  (D表示day，还有W，M，Y，s，m，h，年月日天大写，时分秒小写)<br>
  注1：从字符串创建 datetime64 类型时，默认情况下，numpy 会根据字符串自动选择对应的单位。<br>
  `a = np.datetime64('2020-03', 'D')` <br>
  `print(a, a.dtype)  # 2020-03-01 datetime64[D]`<br>
  (指定为Y就只有2020)<br>
  注2：从字符串创建 datetime64 类型时，可以强制指定使用的单位，如果指定的比写的长，长出来的部分默认最小单位，短则直接截断。<br>
  `print(np.datetime64('2020-03') == np.datetime64('2020-03-01'))  # True`<br>
  `print(np.datetime64('2020-03') == np.datetime64('2020-03-02'))  #False`<br>
  注3：一个比较的例子，numpy中，2020-03和2020-03-01实际上表示同一个时间。事实上，如果两个 datetime64 对象具有不同的单位，它们可能仍然代表相同的时刻。并且从较大的单位（如月份）转换为较小的单位（如天数）是安全的。<br>
  `a = np.arange('2020-08-01 20:00', '2020-08-10', dtype=np.datetime64)`<br>
  注4：用range()可以生成日期范围的数组，如果起始时间和结束时间单位不一样，统一化成小的那一个，如上例，转成分钟m。<br><br>
  
* 时间增量(时间运算)<br>
  datatime64运算结果是timedelta64型的，单位不同时化成小的那个。<br>
  注意，年Y和月M不能和其他单位作运算，两者之间可以。(想想为什么?)<br>
  并且，除法运算的结果没有单位。<br>
  `a = np.timedelta64(1, 'Y')`<br>
  `b = np.timedelta64(6, 'M')`<br>
  `print(a+b) # 18 months`<br>
  `print(a/b) # 2.0`<br><br>

* 数组创建
