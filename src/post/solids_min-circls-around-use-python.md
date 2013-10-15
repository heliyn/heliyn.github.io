title = "最大不覆盖点的圆"
datetime = "2013-10-15 21:09"
tags = ["[solids]","python","好学生","算法"]

----------------------

要求在画布上随机产生十万个点

找到最大的10个能不覆盖产生的点的圆

算法是没想 本来以为会有现成的 结果发现都是图论里的Orz

最终还是把附近点的距离算了遍Orz

再用随机的方法选可能的点排序

试验了几次 在1000x1000的画布上半径最多能到1.42左右

<del>R作图什么的我才不知道呢</del>

```python
#coding:UTF-8

import random
import math
import numpy

dotcount=1000000 #取10000个数
axismax=1000     #坐标限定在[0,1000)
ranr=(dotcount/axismax**2)*2 #考虑附近的点的范围

dots={}
for i in range(dotcount):
  dots[random.random()*axismax]=random.random()*axismax
#取出横坐标排序，方便查找
dotx=dots.keys()
dotx.sort()

#以定的随机性得到点(x,y)满足的半径
def racr(x,y):
  #l为在所有点中横坐标与点相近的点的横坐标
  l=dotx[int((dotcount/axismax)*(x-ranr)):int((dotcount/axismax)*(x+ranr))]
  r=min([math.sqrt((dx-x)**2+(dots[dx]-y)**2) for dx in l])
  return (x,y,r)

#随机取2000个可能的圆心点 找到10个最大半径
#点在[ranr,axismax-rar]之间 过于靠边可能导致点距离计算错误
aty=[('x',float),('y',float),('r',float)]
dic=[racr(max(ranr,random.random()*axismax),min(axismax-ranr,\
     random.random()*axismax)) for i in range(200)]
ath=numpy.array(dic,dtype=aty)
resum=list(numpy.sort(ath,order=['r']))
#输出结果为(点横坐标,点纵坐标,半径)
print resum[-10:]
```
