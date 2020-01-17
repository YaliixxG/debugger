# 浏览器兼容相关

1. *在IE中，无法使用CSS3的混合模式 `mix-blend-mode `*

当你的图片是需要利用`mix-blend-mode`混合模式来做特效时，建议还是换张图片吧。

2. *在IE中，这种`rgba(255, 255, 255, 0.8)表示法在IE下有时候会失效*

建议还是使用十六进制`#DC7083`来表示颜色。

3. *在IE中，元素使用`margin: 0 auto`出现无法居中的情况*

可以在父元素使用`text-align: center`来实现居中效果。

4. *在IE中，`fetch`可以请求数据并响应，但是拿不到数据*

按照请求的步骤排查，结果发现是`response`的问题。在IE下，`response.body`是不存在的，所以不能拿这个做判断条件。

5. *在IE中，出现空白页面，完全没有任何渲染*

尝试安装`babel-polyfill`，来解决这个问题。因为`ES6`的语法可能会有一部分，低版本浏览器是不支持的，所以需要它来进行转译。从`babel`的官方网站下载，安装到web应用，在头部引入即可。

6. *在IE中，滚动条样式问题，这里我想要的效果是无需出现滚动条，但是仍然可以进行滚动*

-   IE浏览器：-ms-overflow-style: none
    
-   火狐浏览器： overflow: -moz-scrollbars-none
    
-   谷歌浏览器：div: -webkit-scrollbar { width: 0 }