各类消息提醒

1.消息提示——wx.showToast\(OBJECT\)

```js
<span style="font-family:'Comic Sans MS';font-size:18px;color:#333333;">//show.js
//获取应用实例
var app = getApp()
Page({
showok:function() {
wx.showToast({
title: '成功',
icon: 'success',
duration: 2000
})
}
})
</span>
```

2.模态弹窗——wx.showModal\(OBJECT\)

```js
//show.js
//获取应用实例
var app = getApp()
Page({
modalcnt:function(){
wx.showModal({
title: '提示',
content: '这是一个模态弹窗',
success: function(res) {
if (res.confirm) {
console.log('用户点击确定')
} else if (res.cancel) {
console.log('用户点击取消')
}
}
})
}
})
```

3.操作菜单——wx.showActionSheet\(OBJECT\)

```js
//show.js
//获取应用实例
var app = getApp()
Page({
actioncnt:function(){
wx.showActionSheet({
itemList: ['A', 'B', 'C'],
success: function(res) {
console.log(res.tapIndex)
},
fail: function(res) {
console.log(res.errMsg)
}
})
}
})
```

4.指定modal弹出    指定哪个modal,可以通过hidden属性来进行选择。

```css
<!--show.wxml-->
<view class="container" class="zn-uploadimg">
<button type="primary"bindtap="modalinput">modal有输入框</button>
</view>
<modal hidden="{{hiddenmodalput}}" title="请输入验证码" confirm-text="提交" cancel-text="重置" bindcancel="cancel" bindconfirm="confirm">
<input type='text'placeholder="请输入内容" auto-focus/>
</modal>
```

```js
//show.js
//获取应用实例
var app = getApp()
Page({
data:{
hiddenmodalput:true,
//可以通过hidden是否掩藏弹出框的属性，来指定那个弹出框
},
//点击按钮痰喘指定的hiddenmodalput弹出框
modalinput:function(){
this.setData({
hiddenmodalput: !this.data.hiddenmodalput
})
},
//取消按钮
cancel: function(){
this.setData({
hiddenmodalput: true
});
},
//确认
confirm: function(){
this.setData({
hiddenmodalput: true
})
}
})
```



