---
title: React
---

# React

#### 1. _shouldComponentUpdate_

答：（props,state 有更新，是否出触发）这个周期函数必须返回一个布尔值，否则会报错，并且必须写在父容器（父组件），否则无效。

#### 2. _使用`ant-design`时，UI 组件上设置`className={style.xxx}`时，样式无效_

答：如果是修改 UI 组件的样式，需设置为`className="xxx"`，在全局中修改即可生效（:global{...})

#### 3. _在 dva 中使用`this.props.dispatch`报错 \_this.props.dispatch is not a function_

答：引入`connect`,然后再在 `class XXX extends component`上面写`@connect`即可

![示例](../.vuepress/public/imgs/react-01.png)

#### 4. ReactJs 项目本地测试出错：_Failed to compile Module not found does not match the corresponding path on disk_

答：看下是具体哪个文件不匹配名字，手动改下即可

#### 5. _子组件中打印`this.props`为空对象？_

答：因为父组件中没有传递`props`给子组件，所以子组件拿不到...在父组件中传递`props`过来即可。

#### 6. _当使用`antd + dva`时，路由和导航组件无法共同绑定切换_

答： 使用`antd`中的`selectedKeys`来实现这个功能，原理是`selectedKeys`是个数组，数组里面的值是什么，`url`上的路由路径就是什么，导航组件就会展示那个页面。所以我们要根据`this.props.location.path`来拿到路由的路劲，然后我们在赋值给`selectedKeys`，在页面组件加载完成时`componentDidMount`进行调用。但是会出现另外一个小问题，此时还应该在`UNSAFE_componentWillReceiveProps`中调用下这个方法，就是当`props`发生变化时，也需调用这个方法。

```js
//先定义
    constructor(props) {
        super(props)
        this.state = {
        collapsed: false,
        selectedKeys: []
        };
    }
```

```js
//在导航组件中添加此属性
<Menu
    defaultSelectedKeys={['welcome']}
    selectedKeys={this.state.selectedKeys}
    defaultOpenKeys={['sub1']}
    mode="inline"
    theme="dark"
>
    .......
</Menu>
```

```js
//定义方法，拿到 url 路由路径，并赋值给 selectedKeys
  handleSelectKeys = (pathname) => {
    const temp = pathname.split('/')
    const key = temp && temp.length < 2 ? 'welcome' : temp[1]
    this.setState({
      selectedKeys: [key]
    })
  }

//在两个生命周期中都要进行调用
  componentDidMount() {
    this.handleSelectKeys(this.props.location.pathname)
  }

  UNSAFE_componentWillReceiveProps(nextProps) {
    const { props } = this.props
    if (nextProps !== props) {
      this.handleSelectKeys(nextProps.location.pathname)
    }
  }
```

#### 7. _使用`antd`导航栏无选中效果_

答：检查没有效果的导航菜单项目，是不是`key`没有设置好。

```js
<Menu.Item key="admin">
    <Link to="/admin">
        <Icon type="inbox" />
        <span>管理</span>
    </Link>
</Menu.Item>
```

#### 8. 根据下拉框来进行条件渲染时，始终无法加载对应的组件？

答：无状态组件是无法加载的，必须是有状态组件，另外设置状态必须是用`this.setState`来进行设置，否则无法更改状态。
改变下拉框选项值利用`onChange`方法来拿到值，再利用这个值来进行不同组件的渲染。记得要在结构中调用这个方法。

```js
//下拉框
<Select
    placeholder="请选择"
    defaultValue="改变DOM"
    allowClears
    style={{ width: 465 }}
    onChange={this.handleChangeDom}
>
    <Select.Option key="0">DOM0</Select.Option>
    <Select.Option key="1">DOM1</Select.Option>
    <Select.Option key="2">DOM2</Select.Option>
    <Select.Option key="3">DOM3</Select.Option>
    <Select.Option key="4">DOM4</Select.Option>
</Select>
//拿值
handleChangeDom = value => {
    this.setState({
      selectTypeNum: value
    });
    this.selectDom();
  };

//根据值改变DOM
selectDom = () => {
    const selectTypeNum = this.state.selectTypeNum;
    switch (selectTypeNum) {
      case '0':
        return (
          // 位置异常
          DOM0
        );
        break;
        ...
    }
```
