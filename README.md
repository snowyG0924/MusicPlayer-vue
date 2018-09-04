
# 移动端音乐 WebApp
## Build Setup

``` bash
# clone the repo into your disk.
$ git clone https://github.com/bxm0927/music-app.git

# install dependencies
$ npm install

# serve with hot reload at localhost:8080
$ npm run dev

# build for production with minification
$ npm run build
```
## 技术栈
- `Vue`
- `vue-router`
- `vuex`
- `vue-lazyload`
- `better-scroll`
- `Sass(Scss)`
- `ES6`

## 实现细节

主要页面：播放器内核页、推荐页、歌单详情页、歌手页、歌手详情页、排行页、搜索页、添加歌曲页、个人中心页等。

核心页面：播放器内核页

**组件树**

```
<app> ................... 根组件
  <my-player> ........... 全局的播放器内核组件
  <my-header> ........... 头部组件
  <my-tab> .............. 导航栏组件
  <router-view> ......... 路由
    <recommend> ......... 推荐页
    <singer> ............ 歌手页
    <rank> .............. 排行页
    <search> ............ 搜索页
```


