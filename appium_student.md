# Appium+Python学习笔记

## Capability设置

> 客户端与服务端简历的一个json串，这个串包含很多设备信息与操作信息

```yacas
app apk地址
appOackage 包名
appActivity 页面名称
automationName 测试引擎
noReset fullReset 是否重置相关环境例如一些权限申请
unicodeKeyBoard 是否需要输入非英文之外的语言并在测试完成后重置输入法
donStopAppOnReset 首次启动的时候，不停止app 热启动
skipDeviceInitialization 跳关安装，权限设置等操作
```

