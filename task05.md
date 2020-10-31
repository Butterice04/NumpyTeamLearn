### task05：排序、搜索和计数

#### 排序

* numpy.sort(a[, axis=-1, kind='quicksort', order=None]) <br>
1. axis：排序沿数组的（轴）方向，0表示按行，1表示按列，None表示展开来排序，默认为-1，表示沿后的轴排序。 <br>
2. kind：排序的算法，提供了快排'quicksort'、混排'mergesort'、堆排'heapsort'， 默认为‘quicksort'。<br>
3. order：排序的字段名，可指定字段排序，默认为None。<br>
返回一个排好序的副本。<br><br>

* numpy.argsort(a[, axis=-1, kind='quicksort', order=None]) <br>
返回排序后原来数组的索引数组。按值排序，但返回的是索引。<br><br>

* numpy.lexsort(keys[, axis=-1]) <br>
对数组按某一指标排序。<br>
如：`np.lexsort([x[:, 0]])`按第一列的大小对每一行排序。<br><br>

* numpy.partition(a, kth, axis=-1, kind='introselect', order=None)<br>
以索引是 kth 的元素为基准，将元素分成两部分，即大于该元素的放在其后面，小于该元素的放在其前面，这里有点类似于快排。<br><br>

#### 搜索
* numpy.argmax(a[, axis=None, out=None])<br>
对指定axis，返回其最大元素的索引，如果不指定，就把数组压为一维，返回索引。<br><br>

* numpy.argmin(a[, axis=None, out=None])<br>
与上一个类似，返回最小值索引。<br><br>

* numpy.nonzero(a) <br>
返回非零元素下标（坐标），也可指定axis。<br>
可以在括号中放入布尔数组，按布尔值取出对应元素。<br>
小tip:可以通过 `a[nonzero(a)] `得到所有 a中的非零值。<br><br>

* numpy.where(condition, [x=None, y=None]) <br>
满足条件condition，输出x，不满足输出y。<br>
只有 condition ，没有 x 和 y ，则输出满足条件 (即非0) 元素的坐标 (等价于 numpy.nonzero)。这里的坐标以tuple的形式给出。<br><br>

* numpy.searchsorted(a, v[, side='left', sorter=None])<br>
1. a：一维输入数组。当 sorter 参数为 None 的时候， a 必须为升序数组；否则， sorter 不能为空，存放 a 中元素的 index ，用于 反映 a 数组的升序排列方式。<br>
2. v：插入 a 数组的值，可以为单个元素， list 或者 ndarray。<br>
3. side：查询方向，当为 left 时，将返回第一个符合条件的元素下标；当为 right 时，将返回后一个符合条件的元素下标。<br>
4. sorter：一维数组存放 a 数组元素的 index，index 对应元素为升序。<br><br>
 
#### 计数
* numpy.count_nonzero(a, axis=None) <br>
返回数组中非零元个数。<br><br>