# React相关BUG

1. `shouldComponentUpdate` （props,state有更新，是否出触发）这个周期函数必须返回一个布尔值，否则会报错，并且必须写在父容器（父组件），否则无效。