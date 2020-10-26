### task03:数组操作

#### 数组变形
  * 首先给出表示数组维度的属性，`numpy.ndarray.shape`，查询后返回一个元组，元组的长度即数组的维度。<br>
直接对修改shape值就可以改变数组形状。<br>
`x = np.array([1, 2, 9, 4, 5, 6, 7, 8])`<br>
`print(x.shape)  # (8,)`<br>
`x.shape = [2, 4]`<br>
`print(x)`<br>
`# [[1 2 9 4] `<br>
`#  [5 6 7 8]]`<br><br>
  * 得到展开的多维数组的属性（将数组转换为一维的迭代器）`numpy.ndarray.flat`<br><br>
  `x=np.array([[1,2,3],[5,6,7]])`<br>
  `print(x)`<br>
  `# [[ 1  2  3]`<br>
  `#  [ 5  6  7]]`<br>
  `y=x.flat`<br>
  `for item in y:`<br>
    ` print(item)`<br>
    `# 1`<br>
    `# 2`<br>
    `# 3`<br>
    `# 4`<br>
    `# 5`<br>
    `# 6`<br>
  * flatten()函数，返回的是副本。<br>
     括号里可以加上`[order=X]`，其中，`X`可以取`C(按行)/F(按列)/A(原顺序)`。
  * ravel()函数，作用类似，但返回的是视图。
  * 给数组赋予一个新的形状：`numpy.reshape(a, newshape[, order='C'])`，如果newshape=[rows,-1]，自动根据行数确定列数，如果newshape=-1，数组降为一维。<br><br>

#### 数组转置
* numpy.transpose(a, axes=None)和self.T<br>
举个小栗子：<br>
`y=x.T`<br>
`y=np.transpose(x)`<br><br>

#### 更改维度
* 创建数组之后，还可以给它增加**一个**维度，常用于矩阵计算。`numpy.newaxis = None `<br><br>
`y = x[np.newaxis, :]`<br>
数组的维度元组变成（1，原来的维度）<br><br>
`y = x[:, np.newaxis]`<br>
数组的维度元组变成（原来的维度，1）<br><br>
一个小tip：numpy.newaxis = None ，因此可以将numpy.newaxis作为None的别名，这对索引数组很有用。<br><br>
* 删除单维度：numpy.squeeze(a, axis=None)。<br>
**注意，只能删shape=1的维度！**<br>
a表示被操作的数组，axis用于指定要删除的维度，但只能指定单维度，也可以不指定，不指定时，删除所有单维度。<br>
datawhale温馨小tip：在机器学习和深度学习中，通常算法的结果是可以表示向量的数组（即包含两对或以上的方括号形式[[]]），如果直接利用这个数组进行画图 可能显示界面为空。我们可以利用 squeeze() 函数将表示向量的数组转换为秩为1的数组，这样利用 matplotlib 库函数画图时，就可以正常的显示结果了。<br>
`x = np.array([[[0], [1], [2]]])`<br>
`print(x.shape)  # (1, 3, 1) `<br>
`y = np.squeeze(x)`<br>
`print(y.shape) # (3,) `<br>
`print(y)  # [0 1 2]`<br><br>

#### 数组组合
* 首先给出一个拼接函数`numpy.concatenate((a1,a2,...),axis=0,out=None`<br>
axis=0,按原有维度进行拼接；axis=1,a2的元素直接插入a1。看一个小栗子：<br>
`x = np.array([[1, 2, 3], [4, 5, 6]]) `<br>
`y = np.array([[7, 8, 9], [10, 11, 12]]) `<br>
`z = np.concatenate([x, y], axis=0) `<br>
`print(z)`<br>
` # [[ 1  2  3] `<br>
` #  [ 4  5  6] `<br>
` #  [ 7  8  9] `<br>
` #  [10 11 12]] `<br><br>
`z = np.concatenate([x, y], axis=1) `<br>
`print(z) `<br>
`# [[ 1  2  3  7  8  9] `<br>
`#  [ 4  5  6 10 11 12]]`<br><br>
*  numpy.stack(arrays, axis=0, out=None)axis用于指定沿新的轴加入数组。<br>
类似的还有`numpy.vstack(tup)``numpy.hstack(tup)Stack `<br><br>
hstack(),vstack() 分别表示水平和竖直的拼接方式。在数据维度等于1时，比较特殊。而当维度大于或等于2时，它们的作用相当 于 concatenate ，用于在已有轴上进行操作。<br><br>

#### 数组拆分
* 首先给出拆分函数` numpy.split(ary, indices_or_sections, axis=0) `<br>
ary表示被拆分的数组，indice给出从原来的数组的什么位置进行拆分，同时需结合axis，如[1,3]和axis=0表示以原来的行为主进行拆分，原来是三个（1,4）数组组成的二维数组，就拆成四个（1,4）的，如果axis=1，以列为主，就拆成两个有三个（1,1）数组的二维数组和一个有三个（1,2）数组的二维数组。（这里还没太看明白，之后有时间来填坑）<br>
*  按高度垂直切分numpy.vsplit(ary, indices_or_sections) <br><br>
*  按宽度水平切分numpy.hsplit(ary, indices_or_sections) <br><br>

#### 数组平铺
* numpy.tile(A, reps) tile是瓷砖的意思，顾名思义，这个函数就是把数组像瓷砖一样铺展开来。<br>
将原矩阵横向复制<br>
`x = np.array([[1, 2], [3, 4]])` <br>
`print(x) `<br>
`# [[1 2] `<br>
`#  [3 4]]`<br><br>
`y = np.tile(x, (1, 3)) `<br>
`print(y) `<br>
`# [[1 2 1 2 1 2] `<br>
`#  [3 4 3 4 3 4]]`<br><br>
np.tile(x, (**3，1**))就是纵向复制 <br><br>
*  numpy.repeat(a, repeats, axis=None)<br> 
1. axis=0 ，沿着y轴复制，实际上增加了行数。<br> 
2. axis=1 ，沿着x轴复制，实际上增加了列数。<br> 
3. repeats ，可以为一个数，也可以为一个矩阵。<br> 
4. axis=None 时就会flatten当前矩阵，实际上就是变成了一个行向量。<br> 

#### 添加、删除元素
* 查找数组的唯一元素numpy.unique(ar, return_index=False, return_inverse=False,return_counts=False, axis=None)<br>
* 删除元素numpy.delete(arr,obj,axis=None)<br>
arr:输入数组<br> 
obj:被移除的部分，整数或数组<br> 
axis:指定轴，行/列，默认压平。<br> 
* 插入元素numpy.insert(arr,obj,value,axis=None)<br>
arr:目标数组<br> 
obj:目标位置<br> 
value:插入的数值<br> 
axis:维度<br> <br> 
