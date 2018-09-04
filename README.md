
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

**推荐页**

上部分是一个轮播图组件，使用第三方库 `better-scroll` 辅助实现，使用 `jsonp` 抓取 QQ音乐(移动端)数据

下部分是一个歌单推荐列表，使用 `axios + Node.js` 代理后端请求，绕过主机限制 (伪造 headers)，抓取 QQ音乐(PC端)数据

歌单推荐列表图片，使用图片懒加载技术 `vue-lazyload`，优化页面加载速度

为了更好的用户体验，当数据未请求到时，显示 `loading` 组件

**推荐页 -> 歌单详情页**

由于歌手的状态多且杂，这里使用 `vuex` 集中管理歌手状态

这个组件更加注重 UX，做了很多类原生 APP 动画，如下拉图片放大、跟随推动、ios 渐进增强的高斯模糊效果 `backdrop-filter` 等

**歌手页**

左右联动是这个组件的难点

左侧是一个歌手列表，使用 `jsonp` 抓取 QQ音乐(PC端)歌手数据并重组 JSON 数据结构

列表图片使用懒加载技术 `vue-lazyload`，优化页面加载速度

右侧是一个字母列表，与左侧歌手列表联动，滚动固定标题实现

**歌手页 -> 歌手详情页**

复用歌单详情页，只改变传入的参数，数据同样爬取自 QQ音乐

**播放器内核页**

核心组件。用 `vuex` 管理各种播放时状态，播放、暂停等功能调用 [audio API](http://www.w3school.com.cn/tags/html_ref_audio_video_dom.asp)

播放器可以最大化和最小化

中部唱片动画使用第三方 JS 动画库 `create-keyframe-animation` 实现

底部操作区图标使用 `iconfonts`。

抽象了一个横向进度条组件和一个圆形进度条组件，横向进度条可以拖动小球和点击进度条来改变播放进度，圆形进度条组件使用 SVG `<circle>` 元素

播放模式有：顺序播放、单曲循环、随机播放，原理是调整歌单列表数组

歌词的爬取利用 `axios` 代理后端请求，伪造 `headers` 来实现，先将歌词 jsonp 格式转换为 json 格式，再使用第三方库 [`js-base64`](https://github.com/dankogai/js-base64) 进行 Base64 解码操作，最后再使用第三方库 [`lyric-parser`](https://github.com/ustbhuangyi/lyric-parser)对歌词进行格式化

实现了侧滑显示歌词、歌词跟随进度条高亮等交互效果

增加了当前播放列表组件，可在其中加入/删除歌曲

**排行页**

普通组件，没什么好说的

**排行页 -> 歌单详情页**

复用歌单详情页，没什么好说的

**搜索页**

抓数据，写组件，另外，根据抓取的数据特征，做了上拉刷新的功能

考虑到数据量大且频繁的问题，对请求做了节流处理

考虑到移动端键盘占屏的问题，对滚动前的 `input` 做了 `blur()` 操作

对搜索历史进行了 `localstorage` 缓存，清空搜索历史时使用了改装过的 `confirm` 组件

支持将搜索的歌曲添加到播放列表

**个人中心**

将 `localstorage` 中 “我的收藏” 和 “最近播放” 反映到界面上

**其他**

此应用的全部数据来自 QQ音乐，推荐页的歌单列表及歌词是利用 `axios` 结合 `node.js` 代理后端请求抓取的。

全局通用的应用级状态使用 `vuex` 集中管理

全局引入 `fastclick` 库，消除 click 移动浏览器300ms延迟

页面是响应式的，适配常见的移动端屏幕，采用 `flex` 布局




