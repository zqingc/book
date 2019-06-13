微信小程序，如何在返回前一个页面时，执行前一个页面的方法

```js
var pages = getCurrentPages(); // 当前页面
 var beforePage = pages[pages.length - 2]; // 前一个页面
 // console.log("beforePage");
 // console.log(beforePage);
 wx.navigateBack({
     success: function() {
         beforePage.onLoad(); // 执行前一个页面的onLoad方法
     }
 });
```



