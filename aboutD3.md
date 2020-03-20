---
title: D3
---
# Mac

#### 1. *D3.select(this)没有选择到this？*   
答：D3.select(this) 不允许使用箭头函数，否则找不到节点，会显示undefined；需要使用原始的 function 

#### 2. *attr设置样式时，无效 ？*   
答：看下前面同样的样式是否使用了 Style， Style 的优先级要高于 attr, 在做样式变化时要注意这点
 