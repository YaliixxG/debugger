---
title: TypeScript
---
# TypeScript

#### 1. 找不到模块 *.less* ？  
答： 引入less模块是会报找不到模块，此时可以告诉TS检查器。  
```js
// 添加一个文件，声明less模块（externals.d.ts）

declare module '*.less' {
  const resource: {[key: string]: string};
  export = resource;
}

// 然后再在 tsconfig.json配置文件中添加这个文件的路径

// tsconfig.json
{
   compilerOptions: {...}
   includes: [
      './path/to/the/new/file/externals.d.ts'
   ]
}
```
