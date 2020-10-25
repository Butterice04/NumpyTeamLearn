### task03:数组操作

* 数组变形
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

  * 

