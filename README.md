### 这里积累一些平时用的比较多的功能组件，或者是将以前用jq实现的东西改用vue保存下。组件暂时没有进行区分。都放在component目录下。待积累的越来越多的时候再进行分类。

### 1、多级联动效果：lian

> 类似城市三级联动，这个实现了无数级别联动

##### 传入参数

> lists：级联数组
> curId：当前选择的id，一般用于修改功能，传入id。从而得到该id对应的父级联动展示。

##### 级联数据说明

```
let arrData = [
  {id: 1, parent_id: 0, name: '一级'},
  {id: 2, parent_id: 0, name: '一级2'},
  {id: 12, parent_id: 1, name: '二级1'},
  {id: 13, parent_id: 1, name: '二级2'},
  {id: 122, parent_id: 12, name: '三级1'},
  {id: 133, parent_id: 13, name: '三级2'},
  {id: 1335, parent_id: 133, name: '四级1'},
  {id: 1336, parent_id: 133, name: '四级2'}
]
```

### 2、移动端进度条：progress-bar

##### 传入参数

>percent: 当前进度传入


## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).