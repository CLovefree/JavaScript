## [360度全景展示:hand:](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/01.360%E5%BA%A6%E5%85%A8%E6%99%AF%E5%B1%95%E7%A4%BA/index.html)

1. 鼠标拖拽，获取鼠标位置变化
2. 鼠标拖拽与图片号码的关系
   - 正负数
   - l模上图片数量
3. 转换方向，x取负

## 9种焦点图切换:haha:

demo1：[简单](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo1.html)

demo2：[淡入](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo2.html)

demo3：[淡入加淡出](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo3.html)

demo4：[上下运动](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo4.html)——移动父层top值

demo5：[自动播放](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo5.html)

demo6：[自动播放，最后一张和第一张无缝切换:arrow_backward:](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo6.html)

demo7：[左右运动](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo7.html)——一次切一张图

demo8：[手风琴](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo8.html)

demo9：[手风琴平均分配](http://htmlpreview.github.io/?https://github.com/CLovefree/JavaScript/blob/master/%E5%A6%99%E5%91%B3%E8%AF%BE%E5%A0%82demo/02.%E4%B9%9D%E7%A7%8D%E7%84%A6%E7%82%B9%E5%9B%BE%E5%88%87%E6%8D%A2/demo9.html)

## 瀑布流

布局

数据添加

### 第一种：浮动的

数据添加到每一列

每列宽度一致;每列高度不一样

什么时候加载数据？:arrow_forward:

- 可视区拉到li底部
- 怎么知道li底部进入可视区？:arrow_forward:
  - li的top加上自身高度<=scrollTop+可视区height
  - 怎么知道哪一列li最低？:arrow_forward:
    - for循环，只要发现一列的小于



### 第二种：定位的

一个ul中，再定位

数组存放当前列的高度，

再添加的时候添加到最短的列

