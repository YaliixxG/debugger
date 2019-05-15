# React相关BUG

1. *shouldComponentUpdate*  
答：（props,state有更新，是否出触发）这个周期函数必须返回一个布尔值，否则会报错，并且必须写在父容器（父组件），否则无效。

2. *使用`ant-design`时，UI组件上设置`className={style.xxx}`时，样式无效*  
答：如果是修改UI组件的样式，需设置为`className="xxx"`，在全局中修改即可生效（:global{...})  

3. 在dva中使用`this.props.dispatch`报错*_this.props.dispatch is not a function*  
答：引入`connect`,然后再在 `class XXX extends component`上面写`@connect`即可  

![示例](./imgs/react-01.png)

4. ReactJs项目本地测试出错：*Failed to compile Module not found does not match the corresponding path on disk*
答：看下是具体哪个文件不匹配名字，手动改下即可
