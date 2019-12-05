计算显示窗口高度666

```js
var scale = 750/res.screenWidth//比例
var tabBar = (res.screenHeight - res.windowHeight) * scale;//tabBar的高度 rpx
var title = 160;  //title高度 rpx
var body = (res.screenHeight * scale - tabBar - title)/scale
console.log(tabBar,1)
console.log(body)
this.setData({
  offsetHeight: body
})
```



