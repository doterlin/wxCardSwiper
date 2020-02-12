# wxCardSwiper
小程序卡片切换效果组件. 支持异步添加卡片数据, 手势滑动触发.

源码地址: [https://github.com/doterlin/wxCardSwiper](https://github.com/doterlin/wxCardSwiper)

## 使用方法
将本项目文件中的`components/cardSwiper`文件夹复制到你项目的目录下，然后在页面的json配置及页面引入。自定义组件的引入和使用请参考[官方文档](https://developers.weixin.qq.com/miniprogram/dev/framework/custom-component/)。

> 本项目包含组件和页面demo，可直接运行(上滑翻到下一张，下滑回到上一张)。

## 参数

+ **data** `Array` 传入的初始数据数组 
+ **loadmore** `事件` 当需要加载更多数据时出发。

## 示例
![demo效果](/demo.gif)


`yourPage.json`页面配置（下面的路径换成你copy到项目的path）
```json
{
  "usingComponents": {
    "CardSwiper": "/components/cardSwiper/cardSwiper"
  }
}
```

`yourPage.wxml`页面结构
```html
<CardSwiper data="{{swiperData}}" bindloadmore="loadMore"> </CardSwiper>
```

`yourPage.js`页面js
```javascript
Page({
    data: {
        currentPage: 0,
        totalPage: 2,
        swiperData: [{
            name: "page: 0, index: 1"
        },{
            name: "page: 0, index: 2"
        },{
            name: "page: 0, index: 3"
        }]
    },

    loadMore({detail}){
        if(this.data.currentPage >= this.data.totalPage) return; //大于总页数时退出
        wx.request({
            url: 'yourApiurl', //仅为示例，并非真实的接口地址
            data: {
                page: this.data.currentPage,
            },
            success (res) {
                detail.addToList(res.data); //调用detail.addToList将新数据累加到组件内部数据
            }
        })
    }
})

```
更详细示例请参考本项目中`pages/index`页面

## 修改样式
如果样式和结构不能满足展示需求，你需要到cardSwiper组件里自行修改`wxml`和`wxss`代码。