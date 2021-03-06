#### H5的地理定位（JS对象来实现定位）

使用场景（LBS环境中：local based services）基于本地服务的应用中：

1. 社交（近场服务）陌陌 、微信摇一摇
2. 导航软件：高德、百度地图、凯立德、腾讯地图，滴滴打车
3. 生活服务类：外卖软件、订票、旅游
4. 健康类的应用：跑步，咕咚，悦跑圈，keep

以上服务获取用户位置可以划分为两大类：

1. 只需要获取一次用户位置    1，3  类似于延时器（只执行一次）
2. 要不断的获取用户位置   2，4   类似于定时器（要不断的执行）

JS是如何获取位置的？

需要学习一个对象，3个方法 

如何实现定位的？（科普）

1. IP地址    PC端，插网线
2. WiFi地址   无线网络   PC端
3. GPS  （全球定位系统）  北斗卫星导航系统  精度非常高，民用的北斗4-5米，美国的GPS大概是8-10
4. 基站    -手机端

------

本质：用经纬度来确定用户的位置

----navigator----

浏览器对象：BOM对象，获取浏览器的信息，

navigator.userAgent

地理定位对象是它的一个子对象

#### 一、navigator.geolocation 对象下的3个方法

1. 一次性位置

   ```js
   语法：navigator.geolocation.getCurrentPosition(获取成功的函数，获取失败后的函数，配置对象);
   //后两个参数可选
   //完整写法：模板
   navigator.geolocation.getCurrentPosition(function(res){
       //res参数是一个对象，该对象是获取成功后的所有的信息，比如经纬度，海拔，行进方向等等
   },function(err){
       //err返回的是获取位置失败后的对象，通过该对象可以知道具体的错误原因
   },{
       
   });
   ```

   ```js
   //获取成功后，res参数的内容是：
   coords：坐标
   --经度: coords.longitude
   --纬度: coords.latitude
   --准确度: coords.accuracy(以米为单位)
   --海拔: coords.altitude  （GPS支持）
   --海拔准确度: coords.altitudeAcuracy （GPS支持）
   --行进方向: coords.heading （GPS支持）
   --地面速度: coords.speed （GPS支持）
   --时间戳: position.timestamp  获取位置的时间
   //位置获取失败后返回的参数，即err的内容如下
   --失败编号: code
   -- 0 : 不包括其他错误编号中的错误，比如用户拒绝了权限
   -- 1 : 用户拒绝浏览器获取位置信息
   -- 2 : 尝试获取用户信息,但失败了
   -- 3 : 设置了timeout值,获取位置超时了
   ```

2. 连续性位置

   类似于定时器，会不断的获取用户信息。

   ```js
   var pos=navigator.geolocation.watchPosition(获取成功的函数，获取失败后的函数，配置对象);
   //如果要中断位置获取，需要清除它
   navigator.geolocation.clearWatch(pos)
   ```
   使用方式同getCurrentPosition,只是在配置对象中多了个属性：

   ```js
   frequency更新的频率，表示多少时间请求一次，有点类似于定时器的时间间隔
   ```
   
   获取经纬度后转为实际地址的第三方工具：https://www.bejson.com/convert/map/（可以用百度地图转）

#### 二、学习百度地图API实现各种地图场景

首页：
http://lbsyun.baidu.com/

JS文档页：
http://lbsyun.baidu.com/index.php?title=jspopular

开发者秘钥API申请入口：
http://lbsyun.baidu.com/apiconsole/key?application=key

地图示例：http://lbsyun.baidu.com/jsdemo.htm

通过搜狐接口获取当前IP地址：
https://pv.sohu.com/cityjson

##### 使用定位获取用户所在地疫情数据【超纲，仅供了解】

参考地址：https://www.iplayseo.com/feiyan/

教程：https://www.bilibili.com/video/BV1o7411u7Wy/

#### 今日单词

1. geolocation 地理定位
2. getCurrentPostion  获取当前用户位置
3. watchPosition  监听用户位置（不断获取）
4. clearWatch  清除用户位置（类似于清空定时器）
5. coords 坐标
6. longitude 经度
7. latitude 纬度